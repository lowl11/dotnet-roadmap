# Типы данных / Data types

Типы данных в C# можно разделить на 2 категории:
- [Примитивные](primitive.md)
- [Ссылочные](reference.md)

### Boxing / Unboxing
Есть в .NET такое понятие как boxing и unboxing. Что это такое?
- Boxing - когда мы кладем Value Type (примитивное значение) из Stack в Heap
- Unboxing - когда мы наоборот, вытаскиваем Value Type из Heap в Stack

```C#
object boxing = 10; // соверишили boxing
int unboxing = (int)boxing; // соверишил unboxing
```