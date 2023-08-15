# Queue

Класс Queue\<T\> представляет обычную очередь, которая работает по алгоритму FIFO ("первый вошел - первый вышел").

Пример:
```C#
// объявляем очередь
Queue<string> people = new();

// заполняем ее данными
people.Enqueue("item #1");
people.Enqueue("item #2");
people.Enqueue("item #3");

// проходимся по очереди
while (people.Count != 0)
{
    Console.WriteLine(people.Dequeue());
}
```

### Методы коллекции
Метод | Описание
--- | ---
void Clear() | очищает очередь
bool Contains(T item) | возвращает true, если элемент item имеется в очереди
T Dequeue() | извлекает и возвращает первый элемент очереди
void Enqueue(T item) | добавляет элемент в конец очереди
T Peek() | просто возвращает первый элемент из начала очереди без его удаления