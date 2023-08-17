# DRY

DRY - Don't Repeat Yourself

Как понятно из названия, нужно лишь не повторять за собой код.

Например:
```C#
class Person {
    public string LastName { get;set; }
    public string FirstName { get;set; }
}

class Student {
    public string LastName { get;set; }
    public string FirstName { get;set; }
    public int Age { get;set; }
}
```
Здесь код повторяется дважды - в классе Person и в классе Student - LastName и FirstName. Например, поменялось какое-либо правило и теперь мы должны хранить не отдельно фамилию и имя а теперь мы должны их объеденить в FullName, тогда придется это поменять во всех классах где есть фамилия и имя.

Как можно исправить:
```C#
class Person {
    public string LastName { get;set; }
    public string FirstName { get;set; }
}

class Student : Person {
    public int Age { get;set; }
}
```
Если написать так то при изменении этих полей это изменение нужно будет проводить только в одном месте