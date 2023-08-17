# SOLID

SOLID - коллекция принципов и аббривеатура
- S - Single Responsibility / Принцип единой ответственности
- O - Open/Closed / Открытость/Закрытость
- L - Liskov Substitution / Метод подстановки Барбары Лискова
- I - Interface Segregation / Разделение Интефрейса
- D - Dependency Inversion / Инверсия зависимостей

### Single Responsibility
Принцип единой ответственности - класс или модуль имеет только 1 причину для изменений.

Например, у нас есть "репозиторий/дао менеджер" связанный со статьями.
```C#
public record Article(string Title, string Description);

public class ArticleRepository
{

    public void Add(Article article)
    {
        // some code
    }

    public void CreateReport()
    {
        // some code
    }
    
}
```
В нем есть код который манипулирует данными по статьям и так же на основе статей создает некий отчет. Это нарушение принципа единой ответственности т.к. Репозиторий имеет 2 причины для изменений: что то меняется в сущности Article или появились какие-то изменения в работе с их отчетами.
Здесь имеет смысл разделить их на 2 репозитория:
```C#
public record Article(string Title, string Description);

public class ArticleRepository
{

    public void Add(Article article)
    {
        // some code
    }

    public void Update(Article article)
    {
        // some code
    }
    
}

public class ArticleReportRepository
{
    
    public void CreateReport()
    {
        // some code
    }

    public void DeleteReport()
    {
        // some code
    }
    
}
```
Теперь мы имеем 2 разных класса/репозитория которые работают лишь с определенной бизнес-сущностью.

### Open/Closed
Принцип открытости/закрытости - открыто для расширения/закрыто для модификаций.

Например у нас есть герой который умеет атаковать. Атаковать он уммет разными видами оружия.
Давайте вызовем этот код
```C#
public class Hero
{

    public void Attack(string weapon)
    {
        int damage;
        switch (weapon)
        {
            case "Sword":
                Console.WriteLine("Атака мечом");
                damage = 100;
                break;
            case "Axe":
                Console.WriteLine("Атака топором");
                damage = 120;
                break;
            case "Dagger":
                Console.WriteLine("Атака кинжалом");
                damage = 80;
                break;
            default:
                throw new Exception("Undefined weapon!");
        }
        
        Console.WriteLine($"Герой атакует врага и наносит {damage} урона");
    }
    
}
```

```C#
Hero hero = new Hero();
hero.Attack("Sword");

Result:
Атака мечом
Герой атакует врага и наносит 100 урона
```

Вроде как работает, но здесь как раз таки нарушается принцип открыто для расширения, но закрто для модификаций. Если мы захотим добавить новый тип оружия, например - "Staff", то придется редактировать метод Attack и добавлять в него еще один case, а это уже является модификацией.
Для этого добавим например класс оружия (Weapon).
```C#
public record Weapon(string Name, int Damage);
```

Затем перепишем метод Attack
```C#
public class Hero
{

    public Weapon Weapon { get; set; }

    public void Attack()
    {
        if (Weapon == null)
        {
            throw new Exception("Вы не дали герою в руки оружие!");
        }
        
        Console.WriteLine($"Герой атакует врага оружием {Weapon.Name} и наносит {Weapon.Damage} урона");
    }
    
}
```

```C#
// создаем героя
Hero hero = new Hero();

// заводим список оружий
var sword = new Weapon("Меч", 100);
var axe = new Weapon("Топор", 120);
var dagger = new Weapon("Кинжал", 80);
var staff = new Weapon("Посох", 200);

// присваиваем герою оружие
hero.Weapon = staff;

// атакуем
hero.Attack();

Result:
Герой атакует врага оружием Посох и наносит 200 урона
```

С такой реализацией сколько бы видов оружия не было добавлено, класс героя переписывать не придется, а только лишь будет расширение кол-ва оружий.

### Liskov Substitution
Принцип подстановки Барбары Лискова - весь функционал базового класса/интерфейса должен работать у наследников.

Например у нас есть интерфейс авторизации в смартфон который выполняет авторизацию через TouchID или через Pin Code. Скажем что есть смартфон от компании Apple и смартфон от компании Google. Но смартфон от компании Google не имеет функцию авторизации через TouchId.

```C#
public interface ISmartphoneAuth
{

    void UseTouchId();
    void UsePinCode();

}

public class AppleSmartphone : ISmartphoneAuth
{

    public void UseTouchId()
    {
        Console.WriteLine("Use Touch ID by Apple SmartPhone");
    }

    public void UsePinCode()
    {
        Console.WriteLine("Use Pin Code by Apple SmartPhone");
    }
    
}

public class GoogleSmartPhone : ISmartphoneAuth
{

    public void UseTouchId()
        => throw new NotImplementedException();

    public void UsePinCode()
    {
        Console.WriteLine("Use Pin Code by Google SmartPhone");
    }
    
}
```

Теперь воспользуемся обеими вариантами авторизации у смартфонов:
```C#
List<ISmartphoneAuth> smartphones = new();
smartphones.Add(new AppleSmartphoneAuth());
smartphones.Add(new GoogleSmartPhone());

foreach (var smartphone in smartphones)
{
    smartphone.UseTouchId();
    smartphone.UsePinCode();
}
```

Это нарушение принципа LSP потому что смартфоны Google не реализуют или не подразумевают реализацию метода родителя.

Для решения этой проблемы нам нужно воспользоваться разными интерфейсами:
```C#
public interface ISmartphoneAuthPinCode
{
    void UsePinCode();
}

public interface ISmartphoneAuthTouchId
{
    void UseTouchId();
}

public class AppleSmartphoneAuth : ISmartphoneAuthPinCode, ISmartphoneAuthTouchId
{
    public void UseTouchId()
    {
        Console.WriteLine("Use Touch ID by Apple SmartPhone");
    }

    public void UsePinCode()
    {
        Console.WriteLine("Use Pin Code by Apple SmartPhone");
    }
}

public class GoogleSmartPhone : ISmartphoneAuthPinCode
{
    public void UsePinCode()
    {
        Console.WriteLine("Use Pin Code by Google SmartPhone");
    }
}
```

Перепишем наш клиентский код:
```C#
List<ISmartphoneAuthPinCode> pingCodeSmartPhones = new();
pingCodeSmartPhones.Add(new AppleSmartphoneAuth());
pingCodeSmartPhones.Add(new GoogleSmartPhone());

List<ISmartphoneAuthTouchId> touchIdSmartPhones = new();
touchIdSmartPhones.Add(new AppleSmartphoneAuth());
// touchIdSmartPhones.Add(new GoogleSmartPhone()); // <- выдаст ошибку

foreach (var smartphone in pingCodeSmartPhones)
{
    smartphone.UsePinCode();
}

foreach (var smartphone in touchIdSmartPhones)
{
    smartphone.UseTouchId();
}
```

### Interface Segregation
Принцип разделения интерфейса - маленькие и более целенаправленные интерфейсы лучше чем большие и разносторонние.

Например у нас есть репозиторий отвечающий за бизнес сущность - статьи.
```C#
interface ArticleRepository
{
    List<Article> Get(Article article);
    void Add(Article article);
    void Update(Article article);
    void delete(Article article);

    ArticleReport GetReport();
    void AddReport(ArticleReport report);
}
```
Интерфейс нарушает принципы ISP и SRP. Интерфейс слишком большой и его невозможно использовать только для работы с сущностью Article или только с сущностью ArticleReport.

Нужно их разделить:
```C#
interface ArticleRepository
{
    List<Article> Get(Article article);
    void Add(Article article);
    void Update(Article article);
    void delete(Article article);
}

interface ArticleReportRepository
{
    ArticleReport GetReport();
    void AddReport(ArticleReport report);
}
```

### Dependency Inversion
Принцип инверсии зависимости - код бизнес логики или верхнеуровневый код не должен зависеть от нижнеуровневого кода.

Например у нас в проекте есть бизнес сущность - уведомление и оно сейчас отправляет уведомления в Telegram
```C#
public class Telegram
{
    public void Send(string message)
    {
        // some code
    }
}

public class NotificationService
{

    private readonly Telegram _telegram;

    public NotificationService(Telegram telegram)
    {
        _telegram = telegram;
    }

    public void Notify(string message)
    {
        _telegram.Send(message);
    }
    
}
```

Клиентский код:
```C#
NotificationService notificationService = new(new Telegram());
notoficationService.Notfiy("some alert");
```

По сути все работает, но что если заказчик захочет изменить телеграм на почту, WhatsApp или SMS. Или вообще захочет чтобы уведомление отправлялось на все направления сразу. Тогда нам придется редактировать наш код каждый раз когда будет меняться бизнес требование

```C#
public interface IMessenger
{
    void Send(string message);
}

public class Telegram : IMessenger
{
    public void Send(string message)
    {
        // some code
    }
}

public class Whatsapp : IMessenger
{
    public void Send(string message)
    {
        // some code
    }
}

public class Email : IMessenger
{
    public void Send(string message)
    {
        // some code
    }
}

public class NotificationService
{

    private readonly List<IMessenger> _messengers;

    public NotificationService(List<IMessenger> messengers)
    {
        _messengers = messengers;
    }

    public void Notify(string message)
    {
        foreach (var messanger in _messengers)
        {
            messanger.Send(message);
        }
    }
    
}
```

Клиентский код:
```C#
var messangers = new List<IMessenger>();
messangers.Add(new Telegram());
messangers.Add(new Whatsapp());
messangers.Add(new Email());

NotificationService notificationService = new(messangers);
notificationService.Notify("Some alert");
```
