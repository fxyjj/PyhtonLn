# Chapter 4
data object type introduction

## 1 Number

*integer* and *floating point number* included

`+`,`-`,`*`,`/`,`//(整除)`,`%(Remainder)`,`**(幂)` arthmetic operations are allowed between Number Object Type

str(): a function used to convert the data type into **string**

len(): a function used to return the length of the **string**

Sometimes if we wanna know the number of digits of some big number, we could use:

`len(str(1234567890))`

### 1.1 import math

`math` module provide more tools help us deal with number

1. math.pi
 ```import math
	>>> print(math.pi)
	3.141592653589793
	```
2. math.ceil() (向上取整，操作符 `//` 默认往下取整作为整除的结果，如果需要向上取整则需要借助该函数来实现)

	``` 4/3
	1.3333333333333333
	>>> int(4/3)
	1
	>>> math.ceil(4/3)
	2
	>>> 4/-3
	-1.3333333333333333
	>>> 4//-3 #the same as int(4/3)
	-2
	>>> math.ceil(4/-3)
	-1
	```
	3. `math.sqrt(x) & math.pow(x,y)`

### 1.2 import random

`random` module used to generate random number in python

1. `random.random()`

which generates a random float uniformly in the semi-open range [0.0, 1.0).

`from random import *
>>> random()
0.9491859922594974
`

2. `random.randrange(stop) & random.randrange(start, stop[, step])`

Return a randomly selected element from range(start, stop, step). This is equivalent to choice(range(start, stop, step)), but doesn’t actually build a range object.

```>>>randrange(5)
1
>>> randrange(1,100,2) # Odd number from 1 to 99 inclusive  
9
```

3. `random.randint(a, b)`

Return a random integer N such that a <= N <= b. Alias for randrange(a, b+1).

4. `random.choice(seq) & random.choices(seq,weights,k)`

**choices 与 sample的区别是： choices会重复取，而sample不会重复取（重复取即取同一个位置上的元素,如果seq长度小于k或者k为负数，会报错）**

Return a random element from the non-empty sequence seq. If seq is empty, raises *IndexError*.

```
>>> choice([1,2,3,4,5]) # random select from 1 to 5
3
>>> choice(['a','b','c','d','e']) # also applied to character list
'a'
>>> choices(['red','blue','black'],[18,18,2],k=6)
['blue', 'red', 'red', 'blue', 'blue', 'blue']
```

5. `random.sample(population, k, *, counts=None)`

Return a k length list of *unique elements* chosen from the population *sequence or set*. Used for random sampling without replacement.

**Repeated elements can be specified one at a time or with the optional keyword-only counts parameter. 
For example, 
sample(['red', 'blue'], counts=[4, 2], k=5) is equivalent to 
sample(['red', 'red', 'red', 'red', 'blue', 'blue'], k=5).**

```
sample([10,20,30,40,50],k=4)
[20, 30, 10, 50]
```

6.  random.uniform(a, b)

```
>>> uniform(2.0,5.0)
4.372064618163735
```

Return a random *floating point number* N such that a <= N <= b for a <= b and b <= N <= a for b < a.

7. random.shuffle(list)

Shuffle a list or sequence

```
>>> deck = ['im1','im2','im3','im4','im5']
>>>shuffle(deck)
>>> deck
['im5', 'im4', 'im1', 'im2', 'im3']
```

## 2 String

### 2.1 序列操作

1. Index begin from 0,
```
>>> str = 'Spam'
>>> len(str)
4
>>> str[0]
'S'
>>> str[1]
'p'
>>> str[2]
'a'
>>> str[3]
'm'
```

2. Reverse Index, the last index refer to len(str)-1 or -1,

```
>>> str[-1]
'm'
>>> str[-2]
'a'
>>> str[-3]
'p'
>>> str[-4]
'S'
```
,
```
>>> str[len(str)-1]
'm'
>>> str[-1]
'm'
```

3. Slice, take a piece of sub list from the input sequence

他们的一般形式是 X[i:j]，取出X中偏移量为i，直到但*不包括*偏移量为j的内容。其结果是返回一个新对象，而不是在原来的对象上修改。
分片的默认边界是[0,len(seq)),

```
>>> str = 'IAmAPieceOfShit'
>>> str[4:]
'PieceOfShit'
>>> str[:3]
'IAm'
>>> str[1:2]
'A'
>>> str[1:2] #sub list from [second to third) element.
'A'
>>> str[1:]
'AmAPieceOfShit'
>>> str[:-1]
'IAmAPieceOfShi'
>>> str[1:] # Everything but the first elem
'AmAPieceOfShit'
>>> str[:-1] # Everything but the last elem
'IAmAPieceOfShi'
>>> str[:] # the whole seq
'IAmAPieceOfShit'
```
4. Concatenation(`+`) and Repetition(`*`)

```
>>> str = 'Spam'
>>> str + 'ABC'
'SpamABC'
>>> str * 8
'SpamSpamSpamSpamSpamSpamSpamSpam'
>>> str
'Spam'
>>> 
```

### 2.2 不可变性
字符串类型在python中具有不可变性，与之相同的是*数字*和*元组*类型，即在创建后不能原位置（in place）修改，
对于创建好的字符串对象，不能修改任意引索上的字符，但是可以通过创建一个同名的新对象并修改指定位置上的内容来达到修改的目的，且python在运行时会自动清理旧的对象。

```
>>> str='Spam'
>>> str[0]='A'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
>>> str = 'A'+str[1:]
>>> str
'Apam'
```

紧接着，python中每一个对象都可以分类为可变或者不可变对象。上述的不可变对象包括*数字，字符串和元组*，可变的对象则包括*列表，字典和集合*。

介于灵活的可变性对象，我们也可以借助*list*来修改字符串：

```
>>> str
'Spam'
>>> lstr = list(str)
>>> lstr
['S', 'p', 'a', 'm']
>>> lstr[0]='A'
>>> lstr
['A', 'p', 'a', 'm']
>>> str = ''.join(lstr)
>>> str
'Apam'
```

或者另外一种类型*bytearray*：

```
>>> B = bytearray(b'spam')
>>> B.extend(b'eggs')
>>> B
bytearray(b'spameggs')
>>> B.decode()
'spameggs'
```

### 2.3 Unique method(functions that depend and operate on objects.)

1. str.find(sub[, start[, end]])

Return the *lowest index* in the string where substring sub is found within the slice s[start:end]. 
Optional arguments start and end are interpreted as in slice notation. *Return -1 if sub is not found*.

```
>>> str='IamAGoodBoy'
>>> 'am' in str
True
>>> 'Gd' in str
False
>>> str.find('am')
1
>>> str1 = 'abcagabg'
>>> str1.find('ab') # return only the index that the substring's first appearance
0
```
To check if a string is a substr of the other one, use `in` operator instead.

2.  str.replace(old, new[, count])

Return *a copy of* the string with all occurrences of substring old replaced by new. If the optional argument count is given, only the first count occurrences are replaced

```
>>> str1 = 'abcagabg'
>>> str1.find('ab') # return only the index that the substring's first appearance
0
>>> str2 = str1.replace('ab','cd')
>>> str2
'cdcagcdg'
>>> str3 = str1.replace('ab','cd',1)
>>> str3
'cdcagabg'
>>> str4 = str1.replace('ac','cd') #if the substring is not contained in the string, then it will return the original string.
>>> str4
'abcagabg'
>>> print(str1,str2,str3,str4)
abcagabg cdcagcdg cdcagabg abcagabg
```

3. str.split(sep=None, maxsplit=-1)

Return a *list* of the words in the string, using *sep* as the delimiter string. *If maxsplit is given, at most maxsplit splits are done (thus, the list will have at most maxsplit+1 elements)*. If maxsplit is not specified or -1, then there is *no limit on the number of splits (all possible splits are made)*.

    If sep is given, consecutive delimiters are not grouped together and are deemed to delimit empty strings (for example, '1,,2'.split(',') returns ['1', '', '2']). The sep argument may consist of multiple characters (for example, '1<>2<>3'.split('<>') returns ['1', '2', '3']). Splitting an empty string with a specified separator returns [''].

For example:
```
>>> '1,2,3'.split(',')
['1', '2', '3']
>>> '1,2,3'.split(',', maxsplit=1)
['1', '2,3']
>>> '1,2,,3,'.split(',')
['1', '2', '', '3', '']
>>>''.split(' ')
['']
>>> ' '.split(' ')
['','']
```

4. str.title(),str.istitle() & str.upper(),str.isupper() & str.lower(),str.islower()


Return *a titlecased version of the string* where words *start with an uppercase character and the remaining characters are lowercase*;
Return *True* if the string is a titlecased string and there is *at least one character*;
Return *a copy of the string* with all the cased characters 4 converted to *uppercase*;
Return *True* if the string is a uppercased string and there is *at least one uppercased character*;
Return *a copy of the string* with all the cased characters 4 converted to *lowercase*;
Return *True* if the string is a lowercased string and there is *at least one lowercased character*;

which is to say, 

```
>>> ' '.isupper()
False
>>> ' '.islower()
False
>>> ' '.istitle()
False
```

5. str.rstrip([chars]) *，可以用来去除字符串结尾处的换行府*

Return a copy of the string with trailing characters removed. The chars argument is a string specifying the set of characters to be removed. *If omitted or None, the chars argument defaults to removing whitespace*. 
**The chars argument is not a suffix; rather, all combinations of its values are stripped:**

```
>>> '   spacious   '.rstrip()
'   spacious'
>>> 'mississippi'.rstrip('ipz')
'mississ'
```

`str.removesuffix(suffix)` will remove a single suffix string rather than all of a set of characters. For example:

```
>>> 'Monty Python'.rstrip(' Python')
'M'
>>> 'Monty Python'.removesuffix(' Python')
'Monty'
>>> str1
'abcagabg'
>>> str1.rstrip('gba')
'abc'
>>> str1.rstrip('gbac')
''
```

6. call for help

-- dir() 内置函数会列出调用者作用域内形式参数的默认值，且回返回一个列表，包含了对象的所有属性。
-- help() 随Python安装的面向系统代码的接口，可查询函数或饭方法的使用。
```
>>> str1
'abcagabg'
>>> dir(str1)
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isascii', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
>>> help(str1)
No Python documentation found for 'abcagabg'.
Use help() to get the interactive help utility.
Use help(str) for help on the str class.
>>> help(str1.replace)
Help on built-in function replace:
replace(old, new, count=-1, /) method of builtins.str instance
    Return a copy with all occurrences of substring old replaced by new.
      count
        Maximum number of occurrences to replace.
        -1 (the default value) means replace all occurrences.  
    If the optional argument count is given, only the first count occurrences are
    replaced.
(END)
```

help相较于dir 而言，在返回相同的函数列表的同时，还会提供完整的类型细节，并且允许查询具体的一个方法。

7. 反斜杠与引号
 *反斜杠*表示特殊的字符，例如: `\n`表示换行
字符串可以被包括在*单引号*或*双引号*中，他们是*等价*的，采用不同的引号可以将另一种引号包含在其中。
*三引号*允许包含多行字符。

```
'IamA"Good"Boy'
'IamA"Good"Boy'
>>> "IamA'Good'Boy"
"IamA'Good'Boy"
>>> "iam
  File "<stdin>", line 1
    "iam
       ^
SyntaxError: EOL while scanning string literal
>>> """
... asdmaskd
... asdijei
... aaaaa
... """
'\nasdmaskd\nasdijei\naaaaa\n'
>>> r'C:\text\new'
'C:\\text\\new'
```

字符串前加r表示去掉反斜杠转义机制， 该方法对诸如Windows下的文件路径的表示十分有用。

8. Unicode support
python 支持Unicode字符串形式，从而支持国际化的字符文本。（了解就好）

9. 模式匹配 **//TODO More, Search for module `re`**
	`import re`

## 3. List

**list 的深拷贝与浅拷贝： `l=[[0]*3]*4 创建的数组里面的元素也为数组，里面的数组元素为浅拷贝，即所有的数组元素都指向一个地址，所以修改其中一个元素的值，其他元素的对应位置也会被修改，我们需要使用生成器来辅助创建独立地址的数组对象`**
eg:
```
>>> l = [[0]*3]*4
>>> l
[[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]]
>>> l[0][0]=2
>>> l
[[2, 0, 0], [2, 0, 0], [2, 0, 0], [2, 0, 0]]

>>> l = [[0 for _ in range(3)] for _ in range(4)]
>>> l
[[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]]
>>> l[0][0]=1
>>> l
[[1, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]]
```

任意类型对象的位置相关的有序集合，没有固定大小，且列表可变

### 3.1 Sequence Operation

支持所有字符串的序列操作，区别是其结果是一个list而不是string。

### 3.2 Unique Function

1. list.append(x): Add an item to the end of the list. Equivalent to a[len(a):] = [x]
2. list.pop([index]): Remove the item at the given position in the list, and return it. If no index is specified, a.pop() removes and returns *the last item* in the list

```
>>> lst
[1, 2, 3, 4, 5]
>>> lst.pop(2)
3
>>> lst
[1, 2, 4, 5]
>>> lst.insert(2,3)
>>> lst
[1, 2, 3, 4, 5]
>>> del lst[2]
>>> lst
[1, 2, 4, 5]
```

**Equals to `del list[index]`**

3. list.insert(i,x):Insert an item at a given position. The first argument is the index of the element before which to insert, so a.insert(0, x) inserts at the front of the list, and a.insert(len(a), x) is equivalent to a.append(x)
```
>>> lst
[1, 2, 3, 4, 5]
>>> lst.insert(0,0)
>>> lst
[0, 1, 2, 3, 4, 5]
>>> lst.remove(0)
>>> lst
[1, 2, 3, 4, 5]
>>> lst.insert(1,6)
>>> lst
[1, 6, 2, 3, 4, 5]
```

4. list.remove(x):Remove the *first* item from the list whose value is equal to x. *It raises a ValueError if there is no such item*

5. list.extend(iterable): Extend the list by appending all the items from the iterable. Equivalent to a[len(a):] = iterable

```
>>> lst
[1, 2, 4, 5]
>>> tail = [6,7,8,9]
>>> lst.extend(tail)
>>> lst
[1, 2, 4, 5, 6, 7, 8, 9]
```

6. list.clear(): Remove all items from the list. Equivalent to del a[:].

7. list.count(x): Return the number of times x appears in the list.

8. list.reverse(): Reverse the elements of the list in place.

9.  list.sort(`*`, key=None, reverse=False): Sort the items of the list in place.

10. sum(iterator): return the sum of the elements in the list(kind of iterator), *int and list with mix data type is not allowed*.

### 3.3 Border Check
Even though the list have a flexible dynamic size, using an element that does not exist is not allowed! for example, use x = list[index] where index<0 or index >= len(list) will raise a *IndexError indicating that index out of range*.

### 3.4 嵌套
Python 支持任意的嵌套，list中嵌套dict，dict嵌套list等，实现矩阵就是list嵌套list。**//TODO Numpy**

### 3.5 List Comprehension Expression


## 4. Dictionary
一种映射，具有可变性。通过key来存储对象。

Unlike sequences, which are indexed by a range of numbers, dictionaries are indexed by **keys**, which can be any immutable(不可变的) type; *strings* and *numbers* can always be keys. ***Tuples** can be used as keys if they contain only strings, numbers, or tuples*; if a tuple contains any mutable object either directly or indirectly, it cannot be used as a key. *You can’t use lists as keys, since lists can be modified in place*

### 4.1 Mapping Operation

1. It is best to think of a dictionary as a set of *key: value* pairs, with the requirement that the keys are **unique (within one dictionary)**. 
2. A pair of braces creates an empty dictionary: *{}*. Placing a comma-separated list of key:value pairs within the braces adds initial key:value pairs to the dictionary; this is also the way dictionaries are written on output.

3. The main operations on a dictionary are *storing a value with some key and extracting the value given the key*. 
4. It is also possible to delete a key:value pair with `del`. 
5. If you store using a key that is already in use, the old value associated with that key is *forgotten*. 
6. It is an error to extract a value using a *non-existent key*.


```
>>> dt={}
>>> dt[('first',1)]='apple'
>>> dt
{('first', 1): 'apple'}
>>> dt[('second',2)]='pear'
>>> dt[('third',3)]='peach'
>>> dt[('forth',4)]='mango'
>>> dt
{('first', 1): 'apple', ('second', 2): 'pear', ('third', 3): 'peach', ('forth', 4): 'mango'}

```
#### 4.2 `list(dict)`
returns a list of all the keys used in the dictionary,
if want it sorted, just use **sorted(dict)**

```
list(dt)
[('first', 1), ('second', 2), ('third', 3), ('forth', 4)]
>>> sorted(dt)
[('first', 1), ('forth', 4), ('second', 2), ('third', 3)]

```
dict.keys() could return the keys sequence as well
D.keys() -> a set-like object providing a view on D's keys
```
dt.keys()
dict_keys(['apple', 'pear', 'peach'])
>>> list(dt)
['apple', 'pear', 'peach']
```

#### 4.3 `in` operator used to check whether a given key is in the dictionary.

```
>>> check = ('first',1) in dt
>>> check
True
>>> check = ('first',2) in dt
>>> check
False
```

`dict.get(key, default=None, /) method`
Return the value for key if key is in the dictionary, else default.
``` 
dt.get('apple',0)
1
>>> dt.get('apple',1)
1
>>> dt.get('mango',1)
1
>>> dt.get('mango',0)
0
>>> dt.get('mango')
```

#### 4.4 `dict()`
constructor used to create a dict. it can build dictionaries directly from *sequences of key-value pairs*

```
dt = dict([('sape',4396),('guido',4127),('jack',4098)])
>>> dt
{'sape': 4396, 'guido': 4127, 'jack': 4098}
```

or When the keys are simple strings, can use keyword arguments:

```
>>> dt = dict(apple=1,pear=2,peach=3,banana=4)
>>> dt
{'apple': 1, 'pear': 2, 'peach': 3, 'banana': 4}

```

or, use `zip()`:

```
>>> dt = dict(zip(['apple','pear','peach'],[1,2,3]))
>>> dt
{'apple': 1, 'pear': 2, 'peach': 3}


```

#### 4.5 Looping techniques: dict.items()

1. When looping through dictionaries, the key and corresponding value can be retrieved at the same time using the *items()* method

```
>>> dt
{'apple': 1, 'pear': 2, 'peach': 3, 'banana': 4}
>>> for k,v in dt.items():
...     print(k,v)
... 
apple 1
pear 2
peach 3
banana 4
```
2. When looping through a *sequence*, the position index and corresponding value can be retrieved at the same time using the *enumerate()* function

```
>>> seq = ['apple','pear','peach','banana']
>>> seq
['apple', 'pear', 'peach', 'banana']
>>> for i,elm in enumerate(seq):
...     print(i,elm)
... 
0 apple
1 pear
2 peach
3 banana
```

## 5. Tuple

Imuutable data type in Python

### 5.1 支持list的序列操作，诸如:

```
lst = tuple('abcdefg')
>>> lst
('a', 'b', 'c', 'd', 'e', 'f', 'g')
>>> lst += tuple('hijk')
>>> lst
('a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k')
>>> len(lst)
11
>>> lst.index('f')
5
>>> lst.count('h')
1

```

### 5.2 Why tuple?
没有list那么灵活但是为什么python支持这样的数据类型呢？

tuple提供了一种完整性约束，在程序中若以list形式传递数据集合的话，在传递过程中有可能会被改变，但tuple不能。对于大型程序来说是方便的。

## 6. File
用于调用电脑上存放的外部文件的主要接口。它可以用来读写，文件记录，音频片段，Excel文档，保存邮件等。

### 6.1 创建文件
python中没有特定的字面量语法来创建文件，所以需要利用内置的open函数来创建文件对象。

1. open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, clo
sefd=True, opener=None)

(string)file: file path in computer,a text or byte string giving the name
(string)mode: an optional string that specifies the mode in which the file is opened. It defaults to 'r' which means open for reading in text mode.
Other mode inculdes:
Character Meaning
    --------- ---------------------------------------------------------------
    'r'       open for reading (default)
    'w'       open for writing, truncating the file first
    'x'       create a new file and open it for writing
    'a'       open for writing, appending to the end of the file if it exists
    'b'       binary mode
    't'       text mode (default)
    '+'       open a disk file for updating (reading and writing)
    'U'       universal newline mode (deprecated)
encoding: 编码方式，可以在python读写的时候采用指定的编码方式进行编解码。

```
>>> file = open('data.txt','w')
>>> file.write('Hello\n')
6
>>> file.write('world\n')
6
>>> file.close()
>>> f = open('data.txt','r')
>>> text = f.read()
>>> text
'Hello\nworld\n'
>>> print(text)
Hello
world

>>> text.split('\n') # file contents are always a string
['Hello', 'world', '']
>>> text.split()
['Hello', 'world']
```

2. Binary & Text

Python 3.x 在文件中的文本文件(text)和二进制文件(binary)之间有明显的界限。
文本文件把内容显示为正常的str，在读写时自动执行Unicode编码和解码。
二进制文件把文件显示为特定的字节字符串，允许不修改地访问文件内容

二进制文件在处理多媒体，获取C程序产生的数据等情况下十分有用。
struct模块可以同时创建和解析被打包过的二进制数据来写入一个二进制模式的文件（后续详细讨论）。

**更多关于文件的知识后续继续讨论**

## 7. Set
唯一的不可变的对象的*无序*集合（本身是具有可变性的）

通过set函数来创建，他支持一般的数学集合的操作，集合更像一个无值的字典的键。

```
>>> X = set('Spam')
>>> Y = {'p','a','m'}
>>> X,Y
({'S', 'a', 'p', 'm'}, {'m', 'a', 'p'})
>>> X & Y 																	# Intersection
{'m', 'a', 'p'}
>>> X | Y                                   # Union
{'S', 'm', 'a', 'p'}
>>> X - Y                                   # Difference
{'S'}
>>> X > Y                                   # Superset
True
>>> X == Y
False
>>> set('spam') == set('pasm')              # Oreder-neutral equality tests
True
>>> list(set[1,2,3,1,1])                    # Filtering out duplicates
[1, 2, 3]
```


## Summery

1. *核心*类型： 数字，字符串，数组，元组，字典，文件被称为Python 的核心类型，因为他们是python的一部分，总是有效的。具有特定的语法来创建其对象。

2. 序列(Sequence) 是指具有位置顺序的对象集合体 （包括字符串，数组和元组，他们共同拥有一般的序列操作。）

3. 映射(Mapping) 是指将键与相关值相互关联映射的对象。（字典是唯一的映射对象，映射没有从左至右的位置顺序，他们通过键获取数据。

4. 多态意味着一个操作符‘+’的意义取决于被操作的对象。即不要把代码限制在特定的类型上，使代码自动适应多种类型。



















