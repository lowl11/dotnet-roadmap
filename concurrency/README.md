# Concurrency

**Асинхронность** - Выполнение одним тредом (одним в моменте) нескольких операций. выполняется с помощью ключевых слов async/await. Эти 2 ключевых слова обязтельно всегда идут вместе с любым методом.

**Многопоточность / Параллелизм** - выполнение нескольких операций в одно и то же время разными потоками

Пример:
```C#
async Task Print()
{
    await Task.Run(() => Console.WriteLine("Hello world"));
}
```

Запуск нескольких поток и дожидания всех (как WaitGroup в Go)
```C#
// определяем и запускаем задачи
var task1 = PrintAsync("Hello World #1");
var task2 = PrintAsync("Hello World #2");
var task3 = PrintAsync("Hello World #3");
 
// ожидаем завершения всех задач
await Task.WhenAll(task1, task2, task3);

async Task PrintAsync(string message)
{
    await Task.Delay(2000);     // имитация продолжительной операции
    Console.WriteLine(message);
}
```