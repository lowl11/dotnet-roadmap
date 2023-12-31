# Stack

Класс Stack<T> представляет коллекцию, которая использует алгоритм LIFO ("последний вошел - первый вышел"). При такой организации каждый следующий добавленный элемент помещается поверх предыдущего. Извлечение из коллекции происходит в обратном порядке - извлекается тот элемент, который находится выше всех в стеке.

Стек - довольно часто встречаемая структура данных в реальной жизни. Банальные примеры стеков - стопка книг или тарелок, где каждую новую книгу или тарелку помещают поверх предыдущей. А извлекают из этой стопки книги/тарелки в обратном порядке - сначала самую верхнюю и так далее. Другой пример - одежда: допустим, человек выходит на улицу в зимнюю погоду и для этого сначала одевает майку, потом рубашку, затем свитер, и в конце куртку. Когда человек снимает с себя одежду - он делает это в обратном порядке: сначала снимает куртку, потом свитер и так далее.

Пример:
```C#
var employees = new List<string> { "Tom", "Sam", "Bob" };
Stack<string> people = new Stack<string>(employees);
foreach (var person in people) Console.WriteLine(person);
 
Console.WriteLine(people.Count); // 3
```

### Методы коллекции
Метод | Описание
--- | ---
Clear | очищает стек
Contains | проверяет наличие в стеке элемента и возвращает true при его наличии
Push | добавляет элемент в стек в верхушку стека
Pop | извлекает и возвращает первый элемент из стека
Peek | просто возвращает первый элемент из стека без его удаления
bool TryPop(out T result) | удаляет из стека первый элемент и передает его в переменную result, возвращает true, если очередь не пуста и элемент успешно получен.
bool TryPeek(out T result) | передает в переменную result первый элемент стека без его извлечения, возвращает true, если элемент успешно получен.