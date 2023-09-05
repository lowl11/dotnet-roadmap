# Fluent API

Fluent API - набор методов (LINQ) для работы с Entity Framework Core.

```C#
class FluentContext : DbContext
{
    public FluentContext() :base("DefaultConnection")
    {}
 
    public DbSet<Phone> Phones { get; set; }
 
    protected override void OnModelCreating(DbModelBuilder modelBuilder)
    {
        // использование Fluent API
        base.OnModelCreating(modelBuilder);
    }
}
```