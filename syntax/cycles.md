# Циклы / Cycles

### for
Пример:
```C#
List<string> list = new();
list.Add("item #1");
list.Add("item #2");
list.Add("item #3");

for (var i = 0; i < list.Count; i++)
{
    Console.WriteLine($"{i+1}: {list.ElementAt(i)}");
}
```

### foreach
Пример:
```C#
List<string> list = new();
list.Add("item #1");
list.Add("item #2");
list.Add("item #3");

foreach (var item in list)
{
    Console.WriteLine(item);   
}
```

### while
Пример:
```C#
List<string> list = new();
list.Add("item #1");
list.Add("item #2");
list.Add("item #3");

var cnt = 0;
while (cnt < list.Count)
{
    Console.WriteLine(list.ElementAt(cnt++));
}
```

### do while
Пример:
```C#
List<string> list = new();
list.Add("item #1");
list.Add("item #2");
list.Add("item #3");

var cnt = 0;
do
{
    Console.WriteLine(list.ElementAt(cnt++));
} while (cnt < list.Count);
```
