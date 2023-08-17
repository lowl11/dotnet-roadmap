# Наследование

Порождение класса на основе другого с преемственностью полей и функционала родителя. В идеале избегать наследования и не увлекаться дальше 2ух уровней иерархии. Есть 1 абстракция и 2 или более наследников-реализаторов.

Наследование имеет 3 вида:
- Делегация (поручение функционала внешнему коду из внутреннего)
- Агрегация (через конструктор)
- Композиция (через поле класса)

Пример:
```C#
class Person {
    public string LastName { get;set; }
    public string FirstName { get;set; }
    public string? MiddleName { get;set; }
}

class Student : Person {
    public string StudentId { get; set; }
    // + поля от класса Person
}

class Teacher : Person {
    public string TeacherId { get; set; }
    // + поля от класса Person
}
```
Здесь классы **Student** и **Teacher** наследуют от класса **Person**. Если описывать эти классы без наследования то пришлось бы 3 поля "LastName", "FirstName", "MiddleName" описывать и в Student и в Teacher. 

Пример с агрегацией:
```C#
class Person {
    public string LastName { get;set; }
    public string FirstName { get;set; }
    public string? MiddleName { get;set; }
}

class Student {
    private readonly Person _person;
    public string StudentId { get; set; }
    
    // агрегация - наследование через конструктор
    public Student(Person person)
    {
        _person = person;
    }
}
```

Пример с композицией:
```C#
class Person {
    public string LastName { get;set; }
    public string FirstName { get;set; }
    public string? MiddleName { get;set; }
}

class Student {
    private Person person;
    public string StudentId { get; set; }
    
    public Student(Person person)
    {
        ...
    }

    // композиция - наследование через сеттер
    public void SetPerson(Person person) {
        person = person;
    }
}
```