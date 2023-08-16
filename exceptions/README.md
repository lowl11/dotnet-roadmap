# Исключения / Exceptions

Самый базовый тип в C# для исключений - **Exception**.
Свойство класса Exception и всех остальных:
- InnerException: "под"эксепшн который повлиял на вызов данного эксепшна
- Message: текст ошибки
- Source: имя объекта или сборки в котором было исключение
- StackTrace: стек вызовов которое вызвало эксепшн
- TargetSite: метод в котором было исключение

Некоторые включенные исключения:
- DivideByZeroException
- ArgumentOutOfRangeException
- ArgumentException
- IndexOutOfRangeException
- InvalidCastException
- NullReferenceException

### Кастомные исключения
Кастомные исключения должны наследоваться от Exception или от любого другого класса который наследуется от Exception