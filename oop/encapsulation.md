# Инкапсуляция

Любой класс, модуль или часть программы должна быть как "черный ящик". Пользователь этой части кода должен видеть только интерфейс использования им (классом или модулем).

Например, у нас есть класс машины (Car) и мы хотим замерить за какое время она проедем расстояние в 1 км. У нас для этого есть поля объема двигателя и лошиданые силы (_engineSize и _horsePower). Задаем мы их через конструктор.
У класса Car есть только 1 публичный метод - Ride(). То есть, после того как мы задали характеристики машины уже можно опробовать ее и проверить за какое время она проедет 1 км. По сути здесь для того чтобы рассчитать это время нужно еще много переменных для остальных характеристик машины + какие-нибудь промежуточные рассчеты для вычисления времени. Инкапсуляция здесь заключается в том что клиенту который вызывает метод Ride() доступен лишь только он и никакая другая информация.
```C#
public class Car
{

    private string _brand; // Range Rover, Mercedes, BWM
    private string _type; // тип машины - седан, внедорожник
    private int _engineSize; // объем двигателя
    private int _horsePower; // лошадиные силы

    public Car(string brand, string type, int engineSize, int horsePower)
    {
        _brand = brand;
        _type = type;
        _engineSize = engineSize;
        _horsePower = horsePower;
    }

    public void Ride()
    {
        Console.WriteLine($"Машина марки {_brand} типа {_type} начинает ехать!");
        // использовать поля _engineSize и _horsePower для рассчетов за какое время проедет машина 1км
        int roadTimeInSeconds = 1;
        Console.WriteLine($"Машина марки {_brand} типа {_type} проехала расстояние в 1км за {roadTimeInSeconds} секунд!");
    }
    
}
```