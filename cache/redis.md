# Redis

Для того чтобы зарегистрировать конфигурации Redis:
```C#
services.AddStackExchangeRedisCache(options => {
    options.ConfigurationOptions = new ConfigurationOptions()
    {
        EndPoints =
        {
            { "localhost", 6379 },
        },
        DefaultDatabase = 0,
        Password = manager.GetValue<string>("RedisPassword"),
    };
});
```

Класс в котором мы хотим работать с Redis. Нужно подключить интерфейс **IDistributedCache**:
```C#
public class SomeCacheResource
{

    private readonly IDistributedCache _cache;

    public SomeCacheResource(IDistributedCache cache)
    {
        _cache = cache;
    }

    public async Task<string> SomeAction()
    {
        var someResource = await _cache.GetStringAsync(key);
        return someResource;
    }

}
```