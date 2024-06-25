# 📚 Entity Framework (EF)

#### Overview of Entity Framework (EF)

**Introduction**

Entity Framework (EF) is an open-source object-relational mapper (ORM) for .NET applications supported by Microsoft. EF allows developers to work with databases using .NET objects, eliminating the need for most of the data-access code they usually need to write. It supports the following paradigms:

* **Code First**: Define your model in code, which EF will use to create the database schema.
* **Database First**: Generate EF models from an existing database schema.
* **Model First**: Define your model in a visual designer, and EF will generate the database schema from the model.

**Key Features and Functions**

1. **Change Tracking**: EF automatically tracks changes made to the objects retrieved from the database.
2.  **Querying**: Use LINQ (Language Integrated Query) to write expressive and concise queries.

    ```csharp
    var entities = context.Entities
                          .Where(e => e.Name.StartsWith("A"))
                          .ToList();
    ```
3. **Migrations**: EF provides a way to incrementally update the database schema to keep it in sync with the application's data model while preserving existing data.

#### Working with Migrations

Migrations in Entity Framework help manage database schema changes. Here's how you can work with migrations:

1.  **Add a Migration**: Create a new migration based on changes to the data model.

    ```sh
    dotnet ef migrations add InitialCreate
    ```
2.  **Update the Database**: Apply the migration to the database.

    ```sh
    dotnet ef database update
    ```
3.  **Remove a Migration**: If you made a mistake in a migration, you can remove it.

    ```sh
    dotnet ef migrations remove
    ```
4.  **Revert to a Previous Migration**: Roll back to a previous state.

    ```sh
    dotnet ef database update LastGoodMigration
    ```

<mark style="color:red;background-color:orange;">**Importance of Not Deleting Migrations**</mark>

* <mark style="background-color:yellow;">**Historical Record**</mark>: Migrations serve as a historical record of all changes made to the database schema. Deleting migrations can cause loss of this history and make it difficult to track changes.
* <mark style="background-color:yellow;">**Data Integrity**</mark>: Deleting migrations can lead to data loss or corruption. By maintaining a complete set of migrations, you ensure that the database can be reliably updated or rolled back.
* <mark style="background-color:yellow;">**Collaboration**</mark>: In a team environment, migrations help synchronize schema changes. Deleting migrations can disrupt other team members' work and lead to inconsistencies.

#### Generic Repository Pattern

The `GenericRepository<T, TKey>` class is a generic implementation of a repository pattern for CRUD operations in Entity Framework. This pattern provides a centralized way to handle data access logic, making the code more modular, testable, and maintainable. Below are the key aspects and functionalities of the `GenericRepository` class.

**Key Aspects**

* **Generic Implementation**: It is designed to work with any entity type (`T`) and primary key type (`TKey`), making it highly reusable.
* **Dependency Injection**: The repository class is designed to be used with dependency injection, receiving an `AppDbContext` and a logger (`ILogger<GenericRepository<T, TKey>>`) via the constructor.
* **Asynchronous Operations**: The repository supports asynchronous operations, which is essential for non-blocking I/O operations and improving application performance.

**Main Functions**

1.  **CreateAsync**: Adds a new entity to the context and saves changes to the database.

    ```csharp
    public virtual async Task<T> CreateAsync(T entity)
    {
        _logger.LogInformation("Creating a new entity.");
        EntityEntry<T> ret = await _context.Set<T>().AddAsync(entity);
        await _context.SaveChangesAsync();
        ret.State = EntityState.Detached;
        _logger.LogInformation("Entity created successfully.");
        return ret.Entity;
    }
    ```
2.  **UpdateAsync**: Updates an existing entity in the context and saves changes to the database.

    ```csharp
    public virtual async Task<int> UpdateAsync(T entity)
    {
        _logger.LogInformation("Updating an entity.");
        EntityEntry<T>? entry = _context.Entry(entity) ?? throw new KeyNotFoundException("Entity not found");
        entry.State = EntityState.Modified;
        int result = await _context.SaveChangesAsync();
        _logger.LogInformation("Entity updated successfully.");
        return result;
    }
    ```
3.  **InsertOrUpdateAsync**: Inserts a new entity or updates an existing one.

    ```csharp
    public virtual async Task<int> InsertOrUpdateAsync(T entity)
    {
        _logger.LogInformation("Inserting or updating an entity.");
        _context.Update(entity);
        int result = await _context.SaveChangesAsync();
        _logger.LogInformation("Entity inserted or updated successfully.");
        return result;
    }
    ```
4.  **DeleteAsync**: Deletes an entity from the context and saves changes to the database.

    ```csharp
    public virtual async Task<bool> DeleteAsync(T entity)
    {
        _logger.LogInformation("Deleting an entity.");
        EntityEntry<T>? entry = _context.Entry(entity) ?? throw new KeyNotFoundException("Entity not found");
        entry.State = EntityState.Deleted;
        await _context.SaveChangesAsync();
        _logger.LogInformation("Entity deleted successfully.");
        return true;
    }
    ```
5.  **GetById**: Retrieves an entity by its primary key.

    ```csharp
    public virtual T GetById(TKey id)
    {
        _logger.LogInformation("Retrieving an entity by ID: {Id}.", id);
        T entity = _context.Set<T>().Find(id)!;
        if (entity == null)
        {
            _logger.LogWarning("Entity not found for ID: {Id}.", id);
        }
        else
        {
            _logger.LogInformation("Entity retrieved successfully for ID: {Id}.", id);
        }
        return entity;
    }
    ```
6.  **GetByIdAsync**: Retrieves an entity asynchronously by its primary key.

    ```csharp
    public virtual async Task<T> GetByIdAsync(TKey id)
    {
        _logger.LogInformation("Retrieving an entity asynchronously by ID: {Id}.", id);
        T entity = (await _context.Set<T>().FindAsync(id))!;
        if (entity == null)
        {
            _logger.LogWarning("Entity not found for ID: {Id}.", id);
        }
        else
        {
            _logger.LogInformation("Entity retrieved successfully for ID: {Id}.", id);
        }
        return entity;
    }
    ```
7.  **Query**: Returns a queryable collection of entities, allowing for further filtering and querying.

    ```csharp
    public virtual IQueryable<T> Query()
    {
        _logger.LogInformation("Querying entities.");
        return _context.Set<T>().AsNoTracking();
    }
    ```
8.  **ListAll**: Returns a queryable collection of all entities.

    ```csharp
    public virtual IQueryable<T> ListAll()
    {
        _logger.LogInformation("Listing all entities.");
        return _context.Set<T>().AsQueryable();
    }
    ```



Entity Framework streamlines data access in .NET applications by providing an abstraction layer between the application and the database. With its powerful features like LINQ querying, change tracking, and migrations, EF enhances productivity and maintains data integrity. Properly managing migrations is crucial for maintaining a consistent and reliable database schema throughout the lifecycle of an application. The `GenericRepository<T, TKey>` class further simplifies data access patterns, promoting code reusability, maintainability, and testability.
