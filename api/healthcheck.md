# Healthchecks

Healthchecks - инструмент встроенный в .NET для подключения хелсчеков

Для того чтобы подключить нужно добавить сервис:
```C#
services.AddHealthChecks();
```

Так же подключить их в приложение:
```C#
app.UseHealthChecks("/health");
app.MapHealthChecks("/health");
```

Так же хелсчек может проверять подключение к БД или к другим ресурсам:
```C#
services.AddHealthChecks().
        AddCheck<DatabaseHealthcheck>(); // проверка подключения к БД
```