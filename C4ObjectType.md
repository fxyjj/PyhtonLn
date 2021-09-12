# Chapter 4
daject typ3 introduction

## Number

*integer* and *floating point number* included

`+`,`-`,`*`,`/`,`//(整除)`,`%(Remainder)`,`**(幂)` arthmetic operations are allowed between Number Object Type

str(): a function used to convert the data type into **string**

len(): a function used to return the length of the **string**

Sometime if we wanna know the number of digits of some big number, we could use:

`len(str(1234567890))`

### import math

`math` module provide more tools help us deal with number

1. math.pi

	` import math
	>>> print(math.pi)
	3.141592653589793
	`
2. math.ceil() (向上取整，操作符 `//` 默认往下取整作为整除的结果，如果需要向上取整则需要借助该函数来实现)

	` 4/3
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
	`

### import random

`random` module used to generate random number in python

1. `random.random()`

which generates a random float uniformly in the semi-open range [0.0, 1.0).

`from random import *
>>> random()
0.9491859922594974
`

2. `random.randrange(stop) & random.randrange(start, stop[, step])`

Return a randomly selected element from range(start, stop, step). This is equivalent to choice(range(start, stop, step)), but doesn’t actually build a range object.

`>>>randrange(5)
1
>>> randrange(1,100,2) # Odd number from 1 to 99 inclusive  
9
`

3. `random.randint(a, b)`

Return a random integer N such that a <= N <= b. Alias for randrange(a, b+1).

4. `random.choice(seq) & random.choices(seq,weights,k)`

**choices 与 sample的区别是： choices会重复1取，而sample不会重复取（重复取即取同一个位置上的元素）**

Return a random element from the non-empty sequence seq. If seq is empty, raises *IndexError*.

`>>> choice([1,2,3,4,5]) # random select from 1 to 5
3
>>> choice(['a','b','c','d','e']) # also applied to character list
'a'
>>> choices(['red','blue','black'],[18,18,2],k=6)
['blue', 'red', 'red', 'blue', 'blue', 'blue']
`

5. `random.sample(population, k, *, counts=None)`

Return a k length list of *unique elements* chosen from the population *sequence or set*. Used for random sampling without replacement.

**Repeated elements can be specified one at a time or with the optional keyword-only counts parameter. 
For example, 
sample(['red', 'blue'], counts=[4, 2], k=5) is equivalent to 
sample(['red', 'red', 'red', 'red', 'blue', 'blue'], k=5).**

`sample([10,20,30,40,50],k=4)
[20, 30, 10, 50]
`

6.  random.uniform(a, b)

`>>> uniform(2.0,5.0)
4.372064618163735
`

Return a random *floating point number* N such that a <= N <= b for a <= b and b <= N <= a for b < a.

7. random.shuffle(list)

Shuffle a list or sequence

`>>> deck = ['im1','im2','im3','im4','im5']
>>>shuffle(deck)
>>> deck
['im5', 'im4', 'im1', 'im2', 'im3']
`

## String

### 序列操作

1. Index begin from 0,
`>>> str = 'Spam'
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
`

2. Reverse Index, the last index refer to len(str)-1 or -1,

`>>> str[-1]
'm'
>>> str[-2]
'a'
>>> str[-3]
'p'
>>> str[-4]
'S'
`
,
`>>> str[len(str)-1]
'm'
>>> str[-1]
'm'
`

3. Slice, take a piece of sub list from the input sequence

他们的一般形式是 X[i:j]，取出X中偏移量为i，直到但*不包括*偏移量为j的内容。其结果是返回一个新对象，而不是在原来的对象上修改。
分片的默认边界是[0,len(seq)),

`>>> str = 'IAmAPieceOfShit'
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
`
4. Concatenation(`+`) and Repetition(`*`)

`>>> str = 'Spam'
>>> str + 'ABC'
'SpamABC'
>>> str * 8
'SpamSpamSpamSpamSpamSpamSpamSpam'
>>> str
'Spam'
>>> 
`

### 不可变性
字符串类型在python中具有不可变性，与之相同的是*数字*和*元组*类型，即在创建后不能原位置（in place）修改，
对于创建好的字符串对象，不能修改任意引索上的字符，但是可以通过创建一个同名的新对象并修改指定位置上的内容来达到修改的目的，且python在运行时会自动清理旧的对象。

`>>> str='Spam'
>>> str[0]='A'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
>>> str = 'A'+str[1:]
>>> str
'Apam'
`

紧接着，python中每一个对象都可以分类为可变或者不可变对象。上述的不可变对象包括*数字，字符串和元组*，可变的对象则包括*列表，字典和集合*。

介于灵活的可变性对象，我们也可以借助*list*来修改字符串：

`>>> str
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
`

或者另外一种类型*bytearray*：

`>>> B = bytearray(b'spam')
>>> B.extend(b'eggs')
>>> B
bytearray(b'spameggs')
>>> B.decode()
'spameggs'
`

### Unique method(functions that depend and operate on objects.)

1. str.find(sub[, start[, end]])

Return the *lowest index* in the string where substring sub is found within the slice s[start:end]. 
Optional arguments start and end are interpreted as in slice notation. *Return -1 if sub is not found*.

`>>> str='IamAGoodBoy'
>>> 'am' in str
True
>>> 'Gd' in str
False
>>> str.find('am')
1
>>> str1 = 'abcagabg'
>>> str1.find('ab') # return only the index that the substring's first appearance
0
`
To check if a string is a substr of the other one, use `in` operator instead.

2.  str.replace(old, new[, count])

Return *a copy of* the string with all occurrences of substring old replaced by new. If the optional argument count is given, only the first count occurrences are replaced

`>>> str1 = 'abcagabg'
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
`

3. str.split(sep=None, maxsplit=-1)

Return a *list* of the words in the string, using *sep* as the delimiter string. *If maxsplit is given, at most maxsplit splits are done (thus, the list will have at most maxsplit+1 elements)*. If maxsplit is not specified or -1, then there is *no limit on the number of splits (all possible splits are made)*.

    If sep is given, consecutive delimiters are not grouped together and are deemed to delimit empty strings (for example, '1,,2'.split(',') returns ['1', '', '2']). The sep argument may consist of multiple characters (for example, '1<>2<>3'.split('<>') returns ['1', '2', '3']). Splitting an empty string with a specified separator returns [''].

For example:
`
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
`

4. str.title(),str.istitle() & str.upper(),str.isupper() & str.lower(),str.islower()


Return *a titlecased version of the string* where words *start with an uppercase character and the remaining characters are lowercase*;
Return *True* if the string is a titlecased string and there is *at least one character*;
Return *a copy of the string* with all the cased characters 4 converted to *uppercase*;
Return *True* if the string is a uppercased string and there is *at least one uppercased character*;
Return *a copy of the string* with all the cased characters 4 converted to *lowercase*;
Return *True* if the string is a lowercased string and there is *at least one lowercased character*;

which is to say, 

`>>> ' '.isupper()
False
>>> ' '.islower()
False
>>> ' '.istitle()
False
`

5. str.rstrip([chars]) *?*

Return a copy of the string with trailing characters removed. The chars argument is a string specifying the set of characters to be removed. *If omitted or None, the chars argument defaults to removing whitespace*. 
**The chars argument is not a suffix; rather, all combinations of its values are stripped:**

`
>>> '   spacious   '.rstrip()
'   spacious'
>>> 'mississippi'.rstrip('ipz')
'mississ'
`

`str.removesuffix(suffix)` will remove a single suffix string rather than all of a set of characters. For example:

`
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
`

6. call for help

-- dir() 内置函数会列出调用者作用域内形式参数的默认值，且回返回一个列表，包含了对象的所有属性。
-- help() 随Python安装的面向系统代码的接口，可查询函数或饭方法的使用。
`>>> str1
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
`

help相较于dir 而言，在返回相同的函数列表的同时，还会提供完整的类型细节，并且允许查询具体的一个方法。

7. 反斜杠与引号
 *反斜杠*表示特殊的字符，例如: `\n`表示换行
字符串可以被包括在*单引号*或*双引号*中，他们是*等价*的，采用不同的引号可以将另一种引号包含在其中。
*三引号*允许包含多行字符。

`'IamA"Good"Boy'
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
`

字符串前加r表示去掉反斜杠转义机制， 该方法对诸如Windows下的文件路径的表示十分有用。

