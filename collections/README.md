# Коллекции / Collections

### Интерфейсы коллекций
[Интерфейсы](interfaces.md)
- [IEnumerable](ienumerable.md)
- [IQueryable](iqueryable.md)
- [IEnumerator](ienumerator.md)

### Коллекции
- [List](list.md)
- [ArrayList](array_list.md) (inherit List)
- [Dictionary](dictionary.md)
- [Queue](queue.md)
- [SortedList](sorted_list.md)
- [Stack](stack.md)
- [Hashtable](hash_table.md) (inherit Dictionary)
- [BitArray](bit_array.md)


### В чем разница между List и Dictionary?
List и Dictionary это 2 крайности
- List кладет элементы к себе за константное время O(1) но при этом долго ищет элементы внутри себя
- Dictionary кладет к себе элементы довольно долго и затратно, но чтение элементов происходит за константное время O(1)

Остальные же коллекции являются чем-то средним между этими двумя коллекциями