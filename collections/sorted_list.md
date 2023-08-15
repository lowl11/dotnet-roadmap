# SortedList

Если нужна коллекция, отсортированная по ключу, можно воспользоваться SortedList<TKey, TValue> Этот класс сортирует элементы на основе значения ключа. Можно использовать не только любой тип значения, но также и любой тип ключа.

Пример:
```C#
SortedList<int, string> list = new();
list.Add(1, "item #6");
list.Add(3, "item #5");
list.Add(5, "item #4");

list.Add(2, "item #3");
list.Add(4, "item #2");

foreach (var item in list)
{
    Console.WriteLine($"Key: {item.Key}. Value: {item.Value}");
}

Result:
Key: 1. Value: item #6
Key: 2. Value: item #3
Key: 3. Value: item #5
Key: 4. Value: item #2
Key: 5. Value: item #4
```

### Методы коллекции
Метод | Описание
--- | ---
void Add(K key, V value) | добавляет новый элемент в словарь