# Swagger

Пример описания эндпоинта для swagger
```C#
/// <summary>
/// Получение списка всех продуктов
/// </summary>
/// <param name="page">Номер страницы</param>
/// <returns>Список всех продуктов</returns>
/// <response code="200">Успешное получение списка</response>
/// <response code="500">Ошибка на стороне сервера</response>
[HttpGet]
[Route("get/{page:int}")]
[ProducesResponseType(typeof(PageListModel<ProductAdminShortModel>), StatusCodes.Status200OK)]
[ProducesResponseType(typeof(ErrorModel), StatusCodes.Status500InternalServerError)]
[Produces("application/json")]
public async Task<IActionResult> GetByPage(int page = 1)
{
    var products = await _productService.GetByPage(page);
    return Ok(products);
}
```

Описание эндпоинта, входящих параметров (query параметры + тело), ответа и ответных (HTTP) статусов
```C#
/// <summary>
/// Получение списка всех продуктов
/// </summary>
/// <param name="page">Номер страницы</param>
/// <returns>Список всех продуктов</returns>
/// <response code="200">Успешное получение списка</response>
/// <response code="500">Ошибка на стороне сервера</response>
```

Дать swagger понять что возвращает эндпоинт и принимает в себя
```C#
[ProducesResponseType(typeof(PageListModel<ProductAdminShortModel>), StatusCodes.Status200OK)]
[ProducesResponseType(typeof(ErrorModel), StatusCodes.Status500InternalServerError)]
[Produces("application/json")]
```