# Dictionary

Некая "мапа" в C# которая хранит данные в виде "ключ-значение"

Пример:
```C#
Dictionary<int, string> people = new();
people.Add(1, "John");
people.Add(2, "Alex");
people.Add(3, "Sindy");

foreach (var item in people)
{
    Console.WriteLine($"Key: {item.Key}. Value: {item.Value}");
}
```

### Методы коллекции
Метод | Описание
--- | ---
void Add(K key, V value) | добавляет новый элемент в словарь
void Clear() | очищает словарь
bool ContainsKey(K key) | проверяет наличие элемента с определенным ключом и возвращает true при его наличии в словаре
bool ContainsValue(V value) | проверяет наличие элемента с определенным значением и возвращает true при его наличии в словаре
bool Remove(K key) | удаляет по ключу элемент из словаря
bool Remove(K key, out V value) | Другая версия этого метода позволяет получить удленный элемент в выходной параметр
bool TryGetValue(K key, out V value) | получает из словаря элемент по ключу key. При успешном получении передает значение элемента в выходной параметр value и возвращает true
bool TryAdd(K key, V value) | добавляет в словарь элемент с ключом key и значением value. При успешном добавлении возвращает true