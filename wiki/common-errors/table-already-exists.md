# 💥 Table Already Exists

#### Error: Table 'tablename' already exists

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

**Description:** This error may occur when the `Migrations` folder is deleted and recreated, leading to conflicts in the database schema.

**Exception Message:**

```
MySqlConnector.MySqlException: Table 'aspnetroles' already exists
```

**Solution:** To resolve this issue, you can drop the `foodservice` schema and then try running the application again. Follow these steps:

1. Connect to your SQLServer database using a tool like SSMS or via command line.
2.  Execute the following command to drop the `foodservice` schema:

    ```sql
    DROP SCHEMA foodservice;
    ```
3. Run the application again to allow Entity Framework to recreate the schema and apply migrations.

**Example Code:** If you encounter this error while running the following code snippet, the above steps should resolve it:

```csharp
/// <summary>
/// Updates the database migration if there are pending migrations.
/// </summary>
/// <param name="services">The service collection.</param>
public static void UpdateMigrationDatabase(this IServiceCollection services)
{
    // Configure database migration
    using (var scope = services.BuildServiceProvider().CreateScope())
    {
        using (var dbContext = scope.ServiceProvider.GetRequiredService<AppDbContext>())
        {
            if (dbContext.Database.GetPendingMigrations().Any())
            {
                dbContext.Database.Migrate();
            }
        }
    }
}
```

By dropping the schema and retrying, you should be able to avoid conflicts caused by existing tables and ensure a clean migration.

***
