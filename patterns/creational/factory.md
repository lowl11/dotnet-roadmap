# Factory Method

**Factory Method** - порождающий паттерн который предоставляет интерфейс/базовый класс для создания объектов от имени родителя но при этом разрешает использовать любого наследника в замен.

**Проблема:** предположим у нас есть логистическая компания и мы пишем для нее приложение. На первых парах у нас среди транспорта есть только Грузовики, но как только приложение становится популярным мы захотим добавить в список транспорта еще и корабли, машины и т.д. Но наш код уже завязан на грузовиках, по этому будет тяжело все переделывать чтобы еще и участвовали "корабли".

**Решение:** Создать интерфейс/базовый класс для класса который управляет логистикой. У этого интерфейса/класса должен быть метод создания транспорта (createTransport())  который будет возвращать нужный нам транспорт в зависимости от логики логистики.

Например:
```C#
public interface ITransport
{
    void Delivery();
}

public interface ILogistics
{
    ITransport CreateTransport();
}

public class LandLogistics : ILogistics
{
    public ITransport CreateTransport()
    {
        return new Truck();
    }
}

public class SeaLogistics : ILogistics
{
    public ITransport CreateTransport()
    {
        return new Ship();
    }
}

public class Truck : ITransport
{
    public void Delivery()
    {
        Console.WriteLine("Delivery by Truck");
    }
}

public class Ship : ITransport
{
    public void Delivery()
    {
        Console.WriteLine("Delivery by Ship");
    }
}
```

Затем смотрим как это работает в клиентском коде:
```C#
List<ILogistics> logistics = new();
// добавляем столько логистических бизнес логик сколько нужно
logistics.Add(new LandLogistics());
logistics.Add(new SeaLogistics());

// и нам будет все равно, сколько их и каких типов
foreach (var logistic in logistics)
{
    ITransport transport = logistic.CreateTransport();
    transport.Delivery();
}
```