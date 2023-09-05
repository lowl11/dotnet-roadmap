# .NET API

### Контроллер
Каждый контроллер должен быть наследован от **ControllerBase**.
```C#
public abstract class BaseController : ControllerBase
```

Так же каждый контроллер должен иметь атрибут **ApiController**. <br>
Если хотите задать общий URL путь для контроллера можно использовать атрибут **Route("\<URL PATH\>")**
```C#
[ApiController]
[Route("api/v1/product")] <-- базовый путь контроллера
public class ProductController : BaseController
```

### Действие (Эндпоинт/Action)
Эндпоинт описывается как обычный метод, но чаще всего должен возвращать **IActionResult**<br>
Для того чтобы задать эндпоинту "метод" запроса нужно использовать один из атрибутов: **[HttpGet]**, **[HttpPost]**, **[HttpPut]**, **[HttpDelete]** и т.д.
```C#
[HttpGet]
public async Task<IActionResult> GetByPage(int page = 1)
{
    //
}
```

Конкретный путь к эндпоинту можно задать с помощью атрибута **Route("")**<br>
Так же, при указании пути можно указать на параметры в пути. Переменнная-параметр должна находиться в фигурных скобках. Например: **{page}**<br>
Указать тип переменной: **{page:int}**<br>
Если параметр обязательный: **{page:int:required}**
```C#
[HttpGet]
[Route("get/{page:int}")]
public async Task<IActionResult> GetByPage(int page = 1)
{
    //
}
```

Полный вариант:
```C#
[HttpGet]
[Route("get/{page:int}")]
public async Task<IActionResult> GetByPage(int page = 1)
{
    var products = await _productService.GetByPage(page);
    return Ok(products);
}
```


[Про Swagger](swagger.md)
