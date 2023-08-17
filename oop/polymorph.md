# Полиморфизм

Возможность разными классами с общим родителем решать одну и ту же проблему но разными способами.

Например у нас есть абстраткное понятие (класс) - животное (Animal). Которое умеет говорить/издавать звуки и так же у животного есть имя/наименование.
В первую очередь опишем абстрактный класс для животных, которое имеет:
- Имя/наименование
- Способность говорить
```C#
public abstract class Animal
{

    // имя животного
    private readonly string _name;

    // передадим имя через конструктор
    protected Animal(string name)
    {
        _name = name;
    }

    // возможность говорить
    public virtual void Speak()
        => Console.WriteLine($"Животное {_name} собирается говорить");

}
```

Предположим что нам нужно описать 3 вида животных: тигр, волк и слон. Они должны иметь такую же возможность говорить и имя.

```C#
public class Tiger : Animal
{

    // передаем имя животного
    public Tiger() : base("Тигр")
    {
    }

    // реализуем/дополняем умение говорить
    public override void Speak()
    {
        base.Speak();
        Console.WriteLine("Tiger speaks");
    }
    
}
```

Реализуем волка
```C#
public class Wolf : Animal
{
    
    public Wolf() : base("Волк")
    {
    }

    public override void Speak()
    {
        base.Speak();
        Console.WriteLine("Wolf speaks");
    }
    
}
```

То же самое для слона
```C#
public class Elephant : Animal
{
    
    public Elephant() : base("Слон")
    {
    }
    
    public override void Speak()
    {
        base.Speak();
        Console.WriteLine("Elephant speaks");
    }
    
}
```

И теперь нам остается опробовать как работает полиморфизм
Для этого создаем 3 объекта типа Animal но дадим им реализации животных Tiger, Wolf и Elephant
Затем создаем список с животными и как мы видим они все совпадают по типу Animal хотя мы всем указали конкретную и разную реализации.
В конце вызываем метод Speak() у каждого животного
```C#
// создаем 3 объекта типа Animal но с разными реализациями
Animal tiger = new Tiger();
Animal wolf = new Wolf();
Animal elephant = new Elephant();

// заполняем список животными
List<Animal> animals = new()
{
    tiger, wolf, elephant,
};

// хотим чтобы животные говорили
foreach (var animal in animals)
{
    animal.Speak();
}
```