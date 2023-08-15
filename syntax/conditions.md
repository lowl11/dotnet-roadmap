# Условия / Conditions

### if else
Пример:
```C#
var x = 5;
if (x > 5) Console.WriteLine("X is more than 5");
else if (x == 5) Console.WriteLine("X equals 5");
else Console.WriteLine("X is less than 5);
```

### switch case
Пример:
```C#
var x = 5;
switch (x) {
    case 1:
        Console.WriteLine("X equals to 1");
        break;
    case 2:
        Console.WriteLine("X equals to 2");
        break;
    case 5:
        Console.WriteLine("X equals to 5");
        break;
    default:
        Console.WriteLine("X is undefined");
        break;
}
```