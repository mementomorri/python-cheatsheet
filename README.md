Исчерпывающая шпаргалка по Python
===============================

Содержание
--------
**&nbsp;&nbsp;&nbsp;** **1. Наборы:** **&nbsp;** **[`List`](#list)**__,__ **[`Dictionary`](#dictionary)**__,__ **[`Set`](#set)**__,__ **[`Tuple`](#tuple)**__,__ **[`Range`](#range)**__,__ **[`Enumerate`](#enumerate)**__,__ **[`Iterator`](#iterator)**__,__ **[`Generator`](#generator)**__.__  
**&nbsp;&nbsp;&nbsp;** **2. Типы:** **&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**  **[`Type`](#type)**__,__ **[`String`](#string)**__,__ **[`Regular_Exp`](#regex)**__.__


Main
----
__Точка входа__
```python
if __name__ == '__main__':      # Вызывает функцию main(), если файл был запущен как скрипт,
    main()                      # а не импортирован. 
```


List
----
__Список__
```python
<list> = <list>[<slice>]        # Или: <list>[включительное_начало : исключительный_конец : ±шаг]
```

```python
<list>.append(<el>)             # Или: <list> += [<el>]
<list>.extend(<collection>)     # Или: <list> += <collection>
```

```python
<list>.sort()                   # Сортировка по возрастанию в исходном списке.
<list>.reverse()                # Развернуть список в обратном порядке в исходном списке.
<list> = sorted(<collection>)   # Возвращает новый отсортированный список не меняя исходный.
<iter> = reversed(<list>)       # Возвращает новый развернутый список не меняя исходный.
```

```python
sum_of_elements  = sum(<collection>)
elementwise_sum  = [sum(pair) for pair in zip(list_a, list_b)]
sorted_by_second = sorted(<collection>, key=lambda el: el[1])
sorted_by_both   = sorted(<collection>, key=lambda el: (el[1], el[0]))
flatter_list     = list(itertools.chain.from_iterable(<list>))
product_of_elems = functools.reduce(lambda out, el: out * el, <collection>)
list_of_chars    = list(<str>)
```
* **Подробности касательно функций sorted(), min() и max() можно найти в разделе [sortable](#sortable).**
* **Модуль [operator](#operator) предоставляет доступ к функциям itemgetter() и mul() они предоставляют тот же функционал, что и описаные выше [lambda](#lambda) выражения.**

```python
<list>.insert(<int>, <el>)   # Вставляет элемент по индексу и смещает остальные элементы вправо.
<el>  = <list>.pop([<int>])  # Удаляет элемент по индексу и возвращает его или последний эелемент.
<int> = <list>.count(<el>)   # Возвращает число повторов элемента. Также работает на строках.
<int> = <list>.index(<el>)   # Возвращает индекс искомого элемента или возвращает ValueError.
<list>.remove(<el>)          # Удаляет элемент по его значению или возвращает ValueError.
<list>.clear()               # Очищает список удаляя все его элементы. Аналогично для 
                                                                      # словарей и можеств.
```


Dictionary
----------
__Словарь__
```python
<view> = <dict>.keys()                          # Набор ключей словаря отображающих изменения.
<view> = <dict>.values()                        # Набор значений словаря отображающих изменения.
<view> = <dict>.items()                         # Набор пар ключ-значение отображающих изменения.
```

```python
value  = <dict>.get(key, default=None)          # Возвращает значение по-умолчанию, 
                                                # при отсутствии искомого ключа.
value  = <dict>.setdefault(key, default=None)   # Возвращает значение по ключу, если ключ 
                                                # отсутств., то записывает значение по-умолчанию.
<dict> = collections.defaultdict(<type>)        # Возвращает словарь 
                                                # со значениями по-умолчанию типа `<type>()`.
<dict> = collections.defaultdict(lambda: 1)     # Врзвращает словарь со значением по-умолчанию 1.
```

```python
<dict> = dict(<collection>)                     # Создаёт словарь из набора пар ключ-значение.
<dict> = dict(zip(keys, values))                # Создаёт словарь из двух наборов.
<dict> = dict.fromkeys(keys [, value])          # Создаёт словарь из набора ключей.
```

```python
<dict>.update(<dict>)                           # Добавляет пары. Заменяет, если ключ совпал.
value = <dict>.pop(key)                         # Удаляет пару по ключу или возвр. KeyError,
                                                # если ключ отсутствует.
{k for k, v in <dict>.items() if v == value}    # Возвращает ключи хранящие указанное значение.
{k: v for k, v in <dict>.items() if k in keys}  # Возвращает словарь отфильтрованный по
                                                                                # набору ключей.
```

### Counter
__Счётчик__  
  
Используется для подсчета хешируемых объектов.  
Объект типа Counter это неупорядоченная коллекция, в которой элементы хранятся как ключи словаря, а их счетчики являются значениями.
```python
>>> from collections import Counter
>>> colors = ['blue', 'blue', 'blue', 'red', 'red']
>>> counter = Counter(colors)
>>> counter['yellow'] += 1
Counter({'blue': 3, 'red': 2, 'yellow': 1})
>>> counter.most_common()[0]
('blue', 3)
```


Set
---
__Множество__
```python
<set> = set()                                   # `{}` возвращает словарь. Поэтому для создания
                                                # множества используется конструктор set().
```

```python
<set>.add(<el>)                                 # Добавляет элемент, аналогично: <set> |= {<el>}
<set>.update(<collection> [, ...])              # Обновляет множ., аналогично: <set> |= <set>
```

```python
<set>  = <set>.union(<coll.>)                   # Объединение, аналогично: <set> | <set>
<set>  = <set>.intersection(<coll.>)            # Пересечение, аналогично: <set> & <set>
<set>  = <set>.difference(<coll.>)              # Разность, аналогично: <set> - <set>
<set>  = <set>.symmetric_difference(<coll.>)    # Симметрическая разность, аналог.: <set> ^ <set>
<bool> = <set>.issubset(<coll.>)                # Является подмножеством, аналог.: <set> <= <set>
<bool> = <set>.issuperset(<coll.>)              # Является надмножеством, аналог.: <set> >= <set>
```

```python
<el> = <set>.pop()                              # Возвращает случайный элемент из множества.
                                                # Возвращает KeyError, если множество пустое.
<set>.remove(<el>)                              # Удаляет элемент из множества по его значению.
                                                # Возвращает KeyError, если элемент отсутствует.
<set>.discard(<el>)                             # Удаляет элемент из множества по его значению.
                                                # Не возвращает ошибку, если элемент отсутствует.
```

### Frozen Set
__Застывшее множество__  
  
* **Неизменяемо и хэшируемо.**
* **Следвательно, можно использовать как ключ словаря или элемента обычного множества.**
```python
<frozenset> = frozenset(<collection>)
```


Tuple
-----
__Кортеж__  
  
**Кортеж - это неизменяемый и хешируемый аналог списока.**
```python
<tuple> = ()                               # Создаёт пустой кортеж.
<tuple> = (<el>,)                          # Создаёт кортеж из одного элемента, аналогично: <el>,
<tuple> = (<el_1>, <el_2> [, ...])         # Создаёт кортеж из нескольких элементов,
                                           # аналогично: <el_1>, <el_2> [, ...]
```

### Named Tuple
__Именованный кортеж__  
  
**Подкласс кортежа с именованными элементами.**

```python
>>> from collections import namedtuple
>>> Point = namedtuple('Point', 'x y')
>>> p = Point(1, y=2)
Point(x=1, y=2)
>>> p[0]
1
>>> p.x
1
>>> getattr(p, 'y')
2
```


Range
-----
__Последовательность чисел__  
  
**Неизменяемая и хешируемая последовательность чисел.**
```python
<range> = range(stop)                      # Создаёт последовательность 
                                           # до значения `stop`, не включая его.
<range> = range(start, stop)               # Создаёт последовательность от значения `start` 
                                           # до значения `stop`, не включая его.
<range> = range(start, stop, ±step)        # Создаёт последовательность от значения `start` 
                                           # до значения `stop`, с шагом `step`.
```

```python
>>> [i for i in range(3)]
[0, 1, 2]
```


Enumerate
---------
__Нумерация__
```python
for i, el in enumerate(<collection> [, i_start]):
    ...
```


Iterator
--------
__Итератор__  
```python
<iter> = iter(<collection>)                # `iter(<iter>)` вернёт неизменённый итератор.
<iter> = iter(<function>, to_exclusive)    # Последовательность возвращаемых функцией значений
                                           # до 'to_exclusive', но не включая его.
<el>   = next(<iter> [, default])          # Возвращает ошибку StopIteration 
                                           # или значение 'default' в конце.
<list> = list(<iter>)                      # Возвращает список оставщися элементов итератора.
```

### Itertools
__Модуль itertools__  
Itertool — это модуль, который предоставляет различные функции, работающие с итераторами для создания комплексных итераторов.
```python
import itertools as it
```

```python
<iter> = it.count(start=0, step=1)         # Возвращает значения начиная с числа `start`
                                           # бесконечно. Опционально принимает тип `float`.
<iter> = it.repeat(<el> [, times])         # Возвращает указнный элемент бесконечно 
                                           # или `times` раз.
<iter> = it.cycle(<collection>)            # Бесконечно повторяет последовательность из набора.
```

```python
<iter> = it.chain(<coll>, <coll> [, ...])  # Опустошает набор элентов в переданном порядке.
                                           # "Связывает" аргументы вместе, если использовать
                                                                                # list()
<iter> = it.chain.from_iterable(<coll>)    # Опустошает набор элементов внутри набора.
```

```python
<iter> = it.islice(<coll>, to_exclusive)   # Возвращает первые 'to_exclusive' элементов.
<iter> = it.islice(<coll>, from_inc, …)    # `to_exclusive, +step_size`. Индексы могут быть None.
```


Generator
---------
__Генератор__  
  
* **Любая функция содержащая оператор `yield` возвращает генератор.**
* **Генераторы и итераторы взаимозаменяемы.**

```python
def count(start, step):
    while True:
        yield start
        start += step
```

```python
>>> counter = count(10, 2)
>>> next(counter), next(counter), next(counter)
(10, 12, 14)
```


Type
----
__Тип__  
  
* **Всё является объетом.**
* **У каждого объекта есть тип.**
* **Тип и класс объекта это синонимы.**

```python
<type> = type(<el>)                # Или используя свойство: <el>.__class__
<bool> = isinstance(<el>, <type>)  # Или используя функцию `type`: issubclass(type(<el>), <type>)
```

```python
>>> type('a'), 'a'.__class__, str
(<class 'str'>, <class 'str'>, <class 'str'>)
```

#### Некоторые типы объектов не имеют встроенных имёт, поэтому их нужно импортировать, например:
```python
from types import FunctionType, MethodType, LambdaType, GeneratorType, ModuleType
```

### Abstract Base Classes
__Абстрактный базовый класс (ABC)__  
  
**Каждый абстрактный базовый класс определяет набор виртуальных подклассов. Эти классы затем распознаются функциями isinstance() и issubclass() как подклассы ABC, хотя на самом деле это не так. ABC также может вручную решить, является ли конкретный класс его виртуальным подклассом, обычно на основе того, какие методы реализованы в классе. Например, Iterable ABC ищет метод iter(), а Collection ABC ищет iter(), contains() и len().**

```python
>>> from collections.abc import Iterable, Collection, Sequence
>>> isinstance([1, 2, 3], Iterable)
True
```

```text
+------------------+------------+------------+----------------------+
|                  |  Итератор  |    Набор   |  Последовательность  |
+------------------+------------+------------+----------------------+
| list, range, str |     +      |     +      |          +           |
| dict, set        |     +      |     +      |                      |
| iter             |     +      |            |                      |
+------------------+------------+------------+----------------------+
```

```python
>>> from numbers import Number, Complex, Real, Rational, Integral
>>> isinstance(123, Number)
True
```

```text
+--------------------+----------+-------------+----------------+--------------+-------+
|                    |  Число   | Комплексное | Действительное | Рациональное | Целое |
+--------------------+----------+-------------+----------------+--------------+-------+
| int                |    +     |      +      |       +        |      +       |   +   |
| fractions.Fraction |    +     |      +      |       +        |      +       |       |
| float              |    +     |      +      |       +        |              |       |
| complex            |    +     |      +      |                |              |       |
| decimal.Decimal    |    +     |             |                |              |       |
+--------------------+----------+-------------+----------------+--------------+-------+
```


String
------
__Строка__  
  
**Неизменяемая последовательность символов.**

```python
<str>  = <str>.strip()                       # Удаляет все неотображаемые символы и разделители.
<str>  = <str>.strip('<chars>')              # Удаляет переданные символы.
                                             # Аналогично для lstrip/rstrip().
```

```python
<list> = <str>.split()                       # Разделяет строку на список по неотображ. символу.
<list> = <str>.split(sep=None, maxsplit=-1)  # Разделяет строку по разделителю 'sep',
                                             # максимум 'maxsplit' раз.
<list> = <str>.splitlines(keepends=False)    # Разбивает строку на список строк по переносам:
                                             # [\n\r\f\v\x1c-\x1e\x85\u2028\u2029] и \r\n.
<str>  = <str>.join(<coll_of_strings>)       # Объединяет элементы,
                                             # используя строку как разделитель.
```

```python
<bool> = <sub_str> in <str>                  # Проверяет, является ли одна строка
                                             # подстрокой второй.
<bool> = <str>.startswith(<sub_str>)         # Проверяет, начинается ли строка с указанного 
                                             # символа. Опционально принимает кортеж символов.
<int>  = <str>.find(<sub_str>)               # Возвращает начальный индекс искомой строки или -1.
<int>  = <str>.index(<sub_str>)              # Аналогично, но возвращает ValueError
                                                          # при отсутствии искомой строки.
```

```python
<str>  = <str>.lower()                       # Изменяет регистр на нижний. 
                                             # Аналогично для upper/capitalize/title().
<str>  = <str>.replace(old, new [, count])   # Заменятеи 'old' на 'new' максимум 'count' раз.
<str>  = <str>.translate(<table>)            # `str.maketrans(<dict>)` для создания арг. `table`.
```

```python
<str>  = chr(<int>)                          # Конвертирует `int` в строку формата Unicode.
<int>  = ord(<str>)                          # Конвертирунт символ формата Unicode в `int`.
```
* **Используй `'unicodedata.normalize("NFC", <str>)'` на таких строках как `'Motörhead'`, перед тем как сравнивать их с другими строками, поскольку символ `'ö'` может быть записан как один или несколько символов.**
* **Аргумент `'NFC'` конвертирует такие символы в одиночные, тогда как аргумент `'NFD'` конвертирует их в два символа.**

### Property Methods
__Методы свойств строк__
```python
<bool> = <str>.isdecimal()                   # Проверяет на наличие символов [0-9].
                                             # Аналогично [०-९] и [٠-٩].
<bool> = <str>.isdigit()                     # Проверяет на наличие символов [²³¹…]
                                             # и isdecimal().
<bool> = <str>.isnumeric()                   # Проверяет на наличие символов [¼½¾], [零〇一…]
                                             # и isdigit().
<bool> = <str>.isalnum()                     # Проверяет на наличие символов [a-zA-Z…]
                                             # и isnumeric().
<bool> = <str>.isprintable()                 # Проверяет на наличие символов [ !#$%…]
                                             # и isalnum().
<bool> = <str>.isspace()                     # Проверяет на наличие символов 
                                             # [ \t\n\r\f\v\x1c-\x1f\x85\xa0…].
```


Regex
-----
__Регулярные выражения__  
  
**Функции для сопоставления регулярных выражений.**

```python
import re
<str>   = re.sub(<regex>, new, text, count=0)  # Заменяет все случаи совпадения на 'new'.
<list>  = re.findall(<regex>, text)            # Возвращает все найденные совпавшие строки.
<list>  = re.split(<regex>, text, maxsplit=0)  # Разбивает строку используя паттерн как делитель.
<Match> = re.search(<regex>, text)             # Возвращает первый случай совпадения или None.
<Match> = re.match(<regex>, text)              # Ищет только в начале текста.
<iter>  = re.finditer(<regex>, text)           # Возвращает все случаи как объект `Match`.
```

* **Аргумент «new» может быть функцией, которая принимает объект Match и возвращает строку.**
* **Аргумент `'flags=re.IGNORECASE'` может быть применен ко всем функциям.**
* **Аргумент `'flags=re.MULTILINE'` заставляет `'^'` и `'$'` соответствовать началу/концу каждой строки.**
* **Аргумент `'flags=re.DOTALL'` заставляет `'.'` также принимать `'\n'`.**
* **Используй `'\1'` или `'\\1'` для обратной ссылки (`'\1'` возвращает символ с восьмеричным кодом 1).**
* **Добавь `'?'` после `'*'` и `'+'`, чтобы сделать их non-greedy.**
* **`'re.compile(<regex>)'` возвращает объект Pattern работающий со всеми перечисленными выше методами.**

### Match Object
__Объект типа Match__
```python
<str>   = <Match>.group([<group1>, ...])       # Возвращает указанные захваченные группы из
                                                                                  # совпадения.
<str>   = <Match>.group(1)                     # Возвращает часть внутри первых скобок паттерна.
<tuple> = <Match>.groups()                     # Возвращает все захваченные группы из совпадения.
<int>   = <Match>.start()                      # Возвращает начальный индекс совпадения.
<int>   = <Match>.end()                        # Возвращает закрывающий индекс совпадения.
```
