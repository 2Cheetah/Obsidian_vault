# \* and \*\*
#python #list

Оператор \* используется для распаковки списка.
```python
>>> numbers = [2, 1, 3, 4, 7]
>>> more_numbers = [*numbers, 11, 18]
>>> print(*more_numbers, sep=', ')
2, 1, 3, 4, 7, 11, 18
```

- Использование * и ** для передачи аргументов в функцию;
- Использование * и **   для сбора переданных в функцию аргументов;
- Использование ** для принятия только именованных аргументов;
- Использование * при распаковке кортежей;
- Использование * для распаковки итерируемых объектов в список/кортеж;
- Использование ** для распаковки словарей в другие словари.

1. Распаковка в аргументы функции
```python
>>> fruits = ['lemon', 'pear', 'watermelon', 'tomato']
>>> print(fruits[0], fruits[1], fruits[2], fruits[3])
lemon pear watermelon tomato
>>> print(*fruits)
lemon pear watermelon tomato
```

Действие распаковки хорошо видно при использовании функции `print`:
```python
>>> print(l1, l2)
[1, 2, 3, 4] ['a', 'b', 'c']
>>> print(*l1, *l2)
1 2 3 4 a b c
```

Операратор \*\* делает похожую вещь с именованными аргументами:
```python
>>> date_info = {'year': "2020", 'month': "01", 'day': "01"}
>>> filename = "{year}-{month}-{day}.txt".format(**date_info)
>>> filename
'2020-01-01.txt'
```

```python
>>> date_info = {'year': "2020", 'month': "01", 'day': "01"}
>>> track_info = {'artist': "Beethoven", 'title': 'Symphony No 5'}
>>> filename = "{year}-{month}-{day}-{artist}-{title}.txt".format(
...     **date_info,
...     **track_info,
... )
>>> filename
'2020-01-01-Beethoven-Symphony No 5.txt'
```

Объединение словарей:
```python
>>> date_info = {'year': "2020", 'month': "01", 'day': "01"}
>>> track_info = {'artist': "Beethoven", 'title': 'Symphony No 5'}
>>> all_info = {**date_info, **track_info}
>>> all_info
{'year': '2020', 'month': '01', 'day': '01', 'artist': 'Beethoven', 'title': 'Symphony No 5'}
```

