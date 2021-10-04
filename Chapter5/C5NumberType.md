# Chapter5 Number

details about the Number type

## 1. 数字类型

### 1.1 整数

一般整数(32位)与长整数(无限精度)：当需要额外的精度时，整数会被自动转换成长整数 （Python2)

在Python3中， 只有整数一种类型，即上述两种已经被合并在一起了。

### 1.2 浮点数 (浮点数的精度问题可以由小数对象(显示)和分数(运算)对象来解决，参见下面的小数与分数)

浮点数带小数点，或者科学记数法的e或者E

在CPython中采用了C语言中的双精度来实现。

### 1.3 十六，八，二进制

1. Hexadecimal： Begin with Ox(or 0X)
`
hex(I) : translate  an integer to hexadecimal string
`
2. Octal： Begin with 0o(or 0O)
`
oct(I): translate an integer to Octal string
`
3. Binary: Begin with 0b(or 0B)

`bin(I): translate an integer to binary string`

*Then, use `int(str,base)` to translate string to an integer based on the base(16,8 or 2)*

### 1/4complex number(复数)

实部+虚部： 复数在技术上通过一对浮点数来实现，但是复数具有自己的一套运算法则

通过 `complex(real,imag)`来创建。

## 2. 表达式运算符和运算规则

### 2.1 操作符 [参见textbook p147]
 
 * `yield x`  stackoverflow

 * python3 不允许比较混合类型的大小
eg. 
 ```
 >>> 1 > 's'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: '>' not supported between instances of 'int' and 'str'
```
 * 混合运算的运算符优先级
 * 括号分组子表达式
 * 混合类型向上转换
*Python首先将被操作的对象转换成其中最复杂的数据类型，在对相同的数据类型进行算术运算。*
 * 混合运算只适用于数字的运算，一个字符加上一个数字会报错
eg.
```
>>> 1+'s'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
```
**python中多态的意义是指： 操作的意义又被操作的对象来决定**

## 3. 数字的创建

```
>>> a,b=3,4
>>> a
3
>>> b
4
>>> 

```
**Python 中的变量不用提前声名，他们在第一次被赋值时就被创建了，但是在使用变量以前他们必须被赋值过一次，否则会报错。**

## 4. Python中的比较操作

### 4.1 普通比较
```
>>> 1 > 2
False
>>> 1 < 2
True
>>> 1 >= 2
False
>>> 1 <= 2
True
>>> 1 != 2
True
>>> 1 == 2
False
>>> 1 == 2.0
False
>>> 1 <= 2.0
True
>>> 
```
上述例子是普通比较的所有情况，值得注意的是：*在比较操作中，如同之前谈到的，在混合类型的操作中，Python会把被操作的对象转换成其中最复杂的数据类型，再操作同类型的数据*

### 4.2 链式比较
Python允许我们将多个比较联结起来执行范围测试，链式比较是布尔表达式的简写，eg. `A < B < C # Boolean test: A < B and B < C`
```
>>> A,B,C = 2,4,6
>>> A < B < C
True
>>> A < B and B < C
True
>>> 
```
注意在链式比较中必须将其视为布尔测试，eg.
```
>>> 1==2<3 # here is 1 == 2 and 2 < 3, but NOT (1==2: false) < 3 => 0 < 3 => True !!
False
>>> 

```

**需要注意的是， 浮点数的比较不总是会符合预期，如, 
```
>>> 1.1+2.2
3.3000000000000003
>>> 3.3
3.3
>>> 

```
这是因为有限的比特位数不能精确的表示一些浮点数，这种情况需要借助一些工具来实现一些有意义的比较，下面看看除法**


## 5.Python中数字的除法

### 5.1 经典除法和真除法

* `x / y`: 在Python2.X 或更早的版本中这个操作对整数或截取小数部分，对于浮点数会保持余项(小数部分)，在Python3.X中该操作统一为真除法，整数与小数统一保留结果的小数部分

* `X // Y`: 向下取整除。Python2.2 过后新增的操作，该操作不考虑操作对象类型，总是截取结果的小数部分，**其结果取决于操作数的类型（整型操作数返回整型结果，浮点数操作数返回浮点类型，小数部分为0）**

* 如果需要在Python2.X中使用Python3.X中的真除法操作，可以导入__future__ 模块，

```from __future__ import division # in Python2.X
>>> 10 / 4
2.5
```

* `//` 向下取整将结果向他的下层舍入
```>>> 8 / 5
1.6
>>> 8 / -5
-1.6
>>> 8 // 5
1 
>>> 8 // -5
-2
```

例如，`8 / 5 = 1.6, => 1 < 1.6 < 2, then 8 // 5 = 1, 舍入到下层1， 而不是2； 该操作同样适用于负数， 8 / -5 = -1.6, => -2 < -1.6 < -1, 舍入到下层-2， 而不是-1`

* math 模块中的截断与向上向下取整
```
from math import *
>>> from math import *
>>> floor(2.5)
2
>>> ceil(2.5)
3
>>> trunc(2.5)
2
>>> floor(-2.5)
-3
>>> ceil(-2.5)
-2
>>> trunc(-2.5)
-2
```

* round(number,ndigits=None), 保留小数位的函数，遵从四舍五入法则， **ndigits可以为负数，表示在整数部分的四舍五入**

```>>> round(2.58899,4)
2.589
>>> round(2.58899,3)
2.589
>>> round(2.58899,2)
2.59
>>> round(21.58899,2)
21.59
>>> round(21.58899,-2)
0.0
>>> round(21.58899,-1)
20.0
>>> round(206.58899,-1)
210.0
>>> round(206.58899,-2)
200.0
```

* 由于//操作总是向下，所以整数向下趋向于0， 负数向下则远离0， 如果总想使得结果趋向于0取舍，则不管正负数的除法，将结果传入math.trunc() 将小数部分截取即可。

## 6. 整数精度

* Python3.X 支持无限精度整数，Python2.X对于无限度精度整数有一个长整型数据类型，该数据的表达方式是在数据末尾加上一个L， (Python3.X 中将该类型与整型结合了).

* 无限精度整数在运算中要比正常的整数慢许多。

## 7. 按位操作

* logic shift right(>>) and logic shift left(<<): 将数字的二进制位串向右或向左位移指定位，数学意义就是位移几位，就除以/右移(乘以/左移)2 的几次幂。
```
 >>> 2<<4
32
>>> 2 * 2**4
32
>>>
>>> 32 >> 4
2
>>> int(32 * 2**-4)
2
```

* 按位与(`&`)，按位或(`|`)，按位异或(`^`), 按位非(`~`) 其操作对象都是以二进制位串为基础的。

* 整型数字的内置函数bit_length 可以查看其二进制位串的长度
```
>>> l = 8000
>>> l.bit_length()
13
>>> 
```

## 8. Useful Tools

### 8.1 内置

1. pow() 返回指数幂值

```
>>> pow(2,2) # 2的2次幂
4
```

2. abs() 返回绝对值

```
>>> abs(-3)
3
>>> abs(3)
3
```

3. sum(iterable) 返回迭代器内元素的和(一般是list 和 tuple, 集合与字典也可以应用该函数，其中*字典*返回其keys的和,但只有在key为int时可用;*集合*内相同元素只计算一次)
```
>>> sum([1,2,3])
6
>>> sum((1,2,3))
6
>>> sum({1:10,2:20,3:30})
6
>>> dt
{(1, 2): 'a', (1, 1): 'b', (2, 1): 'c', (2, 2): 'd'}
>>> sum(dt)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'tuple'
>>> sum({1,2,2,3,4})
10
```
4. max() & min() 

max(): 返回iterable中的最大值或多个元素中的。
min(): 最小值

```
>>> max(1,2,3,4,5)
5
>>> min(1,2,3,4,5)
1
>>> max([1,2,3,4])
4
>>> min([1,2,3,4])
1
>>> max((1,2,3,4))
4
>>> min((1,2,3,4))
1
>>> max('a','b','c')
'c'
>>> min('a','b','c')
'a'
>>> d
[(1, (1, 1)), (2, (1, 2)), (30, (2, 1)), (5, (2, 2))]
>>> max((elm[1] for elm in d), key = lambda x: x[0]) # 匿名函数在max中的应用， min中同样适用
(2, 1)
```

5. from math import *

* math.pi, 圆周率

* math.e, 自然常数

* math.sin(),math.cos() .. 三角函数

(更多该模块内的函数可以参考上一章)
* math.sqrt() 求平方根 

```>>> import math
>>> math.sqrt(144)
12.0
>>> pow(144,0.5)
12.0
>>> 144**0.5
12.0
```

**math模块为外部组建，其中的函数需要在导入math包过后才能使用，而像abs(),max() 等内置函数位于一个隐藏的命名空间(builtins in Python3, __builtin__ in Python2)内，Python会在该命名空间内自动搜索程序的名称**

6. from random import *

(参见上一章)


## 9.小数

Python2.4 过后引入了小数对象，其名称为*Decimal*，创建小数对象需要导入decimal模块，字面量表达式无法直接创建小数。

**小数对象很像浮点数，但是其具有固定的位数和小数点，换句话说，小数是固定精度的浮点数。**

* from decimal import Decimal

```
>>> from decimal import Decimal
>>> 0.1+0.1
0.2
>>> 0.1+0.1+0.1-0.3
5.551115123125783e-17
>>> Decimal('0.1')+Decimal('0.1')+Decimal('0.1')-Decimal('0.3')
Decimal('0.0')
```
**小数对象对表达固定精度的特性（货币的累加）以及实现更好的数值精度而言，是一个理想的工具**

```
>>> Decimal('0.1')+Decimal('0.10')
Decimal('0.20')
```
*值得注意的是，在创建Decimal小数对象时需要传入一个表示小数的字符串，在混合表达式运算时，Python也会自动将操作书转换为最高精度的小数进行运算。*

* 在后续Python版本中（version>=3.1 or 2.7), 也可以通过

`decimal.Decimal.from_float(1.1)` 来创建小数对象，而最新版本的Python可以直接使用float来创建小数：`Decimal(1.1)`,
**但有时会产生默认且庞大的小数位数**
```
>>> Decimal.from_float(1.2)
Decimal('1.1999999999999999555910790149937383830547332763671875')
>>> Decimal(0.1)
Decimal('0.1000000000000000055511151231257827021181583404541015625')
```

* 设置全局小数精度

decimal.getcontext().prec = 4 (该值不能为负，否则报错：valid range for prec is [1, MAX_PREC])

该操作可以指定**所有创建**的小数保留4为小数。

``` import decimal

>>> decimal.Decimal(1)/decimal.Decimal(7)
Decimal('0.1428571428571428571428571429')

>>> decimal.getcontext().prec=4

>>> decimal.Decimal(1)/decimal.Decimal(7)
Decimal('0.1429')
```

* 上下文管理器 

在python2.6 和 3.0 版本中，with关键词可以临时修改小数精度，在with语句退出时，小数对象会重新应用全局精度。

```
>>> import decimal

>>> decimal.Decimal('1.00')/decimal.Decimal('3.00')
Decimal('0.3333333333333333333333333333')

>>> with decimal.localcontext() as ctx:
...     ctx.prec = 2
...     decimal.Decimal('1.00')/decimal.Decimal('3.00')
... 
Decimal('0.33')

>>> decimal.Decimal('1.00')/decimal.Decimal('3.00')
Decimal('0.3333333333333333333333333333')
>>> 
```

## 10. 分数

2.6 与 3.0 首次引入了Fraction类型，即分数，一个有理数对象，显式地保持一个分子和分母，避免了浮点数在算术运算时的不精确性与局限性。

* 创建
```
>>> x = Fraction(1,3)
>>> y = Fraction(1,6)
>>> x
Fraction(1, 3)
>>> y
Fraction(1, 6)
>>> print(x)
1/3
>>> print(y)
1/6
```
同样类似的，分数也可以通过浮点数字符串来创建

```
>>> Fraction('.5')
Fraction(1, 2)
>>> Fraction('.25')
Fraction(1, 4)
```

* 运算 与其他数值类型等同时之
```
>>> x+y
Fraction(1, 2)
>>> print(x+y)
1/2
>>> print(x-y)
1/6
>>> print(x*y)
1/18
>>> print(x/y)
2
>>> print(Fraction(2,1))
2
```

* 对于在给定内存空间内无法精确表示的值，浮点数的限制很明显，而小数与分数都能提供比浮点数更为直观的和准确的结果，通过有理数表示和限制精度。但是后两者需要一个额外的代码冗余和速度的代价。

* 对于混合类型的表达式，有时候需要手动的传递Fraction才能确保精度
```
>>> x = Fraction(1,3)
>>> x+2.0
2.3333333333333335
>>> x+1./3
0.6666666666666666

>>> x + Fraction(4.,3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/fxyj/anaconda3/lib/python3.7/fractions.py", line 174, in __new__
    raise TypeError("both arguments should be "
TypeError: both arguments should be Rational instances

>>> x + Fraction(4,3)
Fraction(5, 3)
>>>
```
**Fraction 的两个参数（分子和分母）必须为整数**

* 浮点数在转换成分数时有时候会有精度损失，因为有可能这个数在浮点数表示时就不够精确，我们可以限制分数的最大分母来简化该结果：
```
>>> x + Fraction(4,3)
Fraction(5, 3)
>>> f = 2.5
>>> f.as_integer_ratio()
(5, 2)
>>> (4.0/3).as_integer_ratio()
(6004799503160661, 4503599627370496)
>>> fn = (4.0/3).as_integer_ratio()
>>> fnf = Fraction(*fn)
>>> fnf.limit_denominator()
Fraction(4, 3)
>>> 
```
## 11.集合

一些唯一不可变对象的集合体。其中不包含重复元素，即一个元素只能出现一次，不管它被添加多少次。

### 11.1 创建

* set()

```
>>> s = set('abcde')
>>> s
{'e', 'a', 'c', 'd', 'b'}
```
*可以看到元素并没有顺序*

## 11.2 运算

* 集合可以通过表达式运算符支持一般的数学操作（列表字典和元组不行）

```
>>> x = set('abcde')
>>> y = set('bdxyz')
>>> x
{'e', 'a', 'c', 'd', 'b'}
>>> y
{'z', 'd', 'y', 'x', 'b'}

>>> x - y # 差集
{'c', 'a', 'e'}

>>> x | y # 并集
{'z', 'e', 'a', 'c', 'd', 'y', 'x', 'b'}

>>> x & y # 交集
{'d', 'b'}

>>> x ^ y # XOR ( x|y - x&y ,筛选的元素要么在x,要么在y, 不包含共同拥有的元素)
{'c', 'z', 'e', 'y', 'x', 'a'}

>>> x > y # y是否为x的真子集，>= 则包含集合本身
False

>>> x < y # 与上同
False
```

* in 成员测试关键词

in表达式可以应用于所有的集合体类型中，其目的时测试测试成员。

### 11.3 set的方法

* set.add(val), 插入一个元素

* set.update(otherset) 原位置求并集， 即一次性加入多个元素（相同元素只记一次）

* set.remove(val) 根据值val删除一个元素, val 若不在集合中，会报错KeyError

* set.union(otherset), 与 & 相同

* set.intersection(otherset), 与 | 相同

* set. issubset(otherset), 判断`set < otherset`

```
>>> x
{'e', 'a', 'c', 'd', 'b'}
>>> y
{'z', 'd', 'y', 'x', 'b'}

>>> x.remove('f')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'f'

>>> x.intersection(y)
{'d', 'b'}
>>> y.intersection(x)
{'d', 'b'}
>>> x & y
{'d', 'b'}

>>> x.union(y)
{'z', 'e', 'a', 'c', 'd', 'y', 'x', 'b'}
>>> y.union(x)
{'z', 'e', 'a', 'c', 'd', 'y', 'x', 'b'}
>>> x | y
{'z', 'e', 'a', 'c', 'd', 'y', 'x', 'b'}


>>> x.remove('f')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'f'
>>> x.remove('a')
>>> x
{'e', 'c', 'd', 'b'}

>>> x.add('a')
>>> x
{'e', 'a', 'c', 'd', 'b'}

>>> x.update(y)
>>> x
{'z', 'e', 'a', 'c', 'd', 'y', 'x', 'b'}

>>> x - y 
{'c', 'a', 'e'}

>>> x .remove(y)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: {'z', 'd', 'y', 'x', 'b'}

>>> x
{'z', 'e', 'a', 'c', 'd', 'y', 'x', 'b'}
>>> x = x - y
>>> x
{'c', 'a', 'e'}
>>> y
{'z', 'd', 'y', 'x', 'b'}
>>> x.issubset(y)
False
>>> x < y
False
```

### 11.4 集合字面量

* Python3.X 中可以使用花括号来创建集合，便于创建结构已知的集合。
* 但是在**所有**Python版本中，**花括号 {} 都表示字典**，所以空的集合不能通过字面量的方式来创建，只能通过set函数

* 通过字面量创建的集合的方法与上述使用set创建的集合所有方法都通用，但是字面量集合的一些方法可以支持表达式不支持的可迭代对象操作数。
```
>>> x = set([1,2,3,4])
>>> x
{1, 2, 3, 4}

>>> {1,2,3} | {3,4}
{1, 2, 3, 4}

>>> {1,2,3} | [3,4]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for |: 'set' and 'list'

>>> {1,2,3}.union({3,4})
{1, 2, 3, 4}

>>> {1,2,3}.union([3,4])
{1, 2, 3, 4}

>>> {1,2,3}.union((3,4))
{1, 2, 3, 4}

>>> {1,2,3}.union(dict(zip([3,4],['a','b'])))
{1, 2, 3, 4}

# union和intersection,issubset方法支持参数类型 集合，数组，元组，字典(字典的键值进行运算)等 
```

* set.copy()
```
>>> x = {1,2,3}
>>> s = x.add(30)
>>> s

>>> x
{1, 2, 3, 30}
>>> s = x
>>> s
{1, 2, 3, 30}

>>> x.remove(30) # 浅拷贝对象s直接指向x的数据地址，所以在x被修改过后s也会变成新的x的值
>>> s
{1, 2, 3}

>>> s = x.copy() # copy函数会为s创建一个副本，有自己的物理地址，所以x被修改后不会影响到s
>>> s
{1, 2, 3}
>>> x.add(30)
>>> x
{1, 2, 3, 30}
>>> s
{1, 2, 3}
>>> 
```

### 11.5 不可变性限制与冻结集合

* **集合内的元素必须是不可变的（数字或者字符串，元组），其中元组在集合操作中会比较其完整的值。**

```
>>> S = set([1,2,3,4,(1,2,3),(4,5,6)])

>>> S
{1, 2, 3, 4, (1, 2, 3), (4, 5, 6)}
>>> (1,2,3) in S
True
>>> (1,5,3) in S
False

>>> S.add([1,7,3])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'

>>> S.add({1,7,3})
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'set'

>>> S.add({1:'a',7:'b',3:'c'})
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'dict'

>>> S.add((1,7,3))

>>> S
{1, 2, 3, 4, (1, 2, 3), (1, 7, 3), (4, 5, 6)}
>>> 
```

* frozenset(),用来创建一个不可变的集合对象，可以用来嵌入到其他集合中。

```
>>> fS = frozenset([1,2,3])
>>> fS
frozenset({1, 2, 3})

>>> type(fS)
<class 'frozenset'>

>>> set(dir(S)) - set(dir(fS))
{'update', 'intersection_update', 'clear', 'pop', '__isub__', 'difference_update', 'remove', 'discard', 'add', 'symmetric_difference_update', '__iand__', '__ior__', '__ixor__'}
>>> 

```

*可以看到frzonset类型中没有可以修改set的方法，诸如 add,update,remove 等*

### 11.6 集合在Python的实用意义

* 过滤集合体中的重复项

* 比较集合体之间的差异

* 进行一些与顺序无关的等价性测试

```
>>> l1,l2 = [1,2,3,4,5],[1,3,4,2,5]
>>> l1==l2
False
>>> set(l1)==set(l2)
True
>>> sorted(l1)==sorted(l2)
True
>>> l2.sort()
>>> l2
[1, 2, 3, 4, 5]
>>> l1
[1, 2, 3, 4, 5]
>>> reverse(l1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'reverse' is not defined
>>> reversed(l1)
<list_reverseiterator object at 0x7f23c4178890>
>>> print(reversed(l1))
<list_reverseiterator object at 0x7f23c41788d0>
>>> for elm in reversed(l1):
...     print(elm)
... 
5
4
3
2
1
>>> l1.reverse()
>>> l1
[5, 4, 3, 2, 1]
>>> 'apsm'=='spam',set('asmp')==set('spam')
(False, True)
>>> 
```
* **由于集合不关心元素的顺序，所以在集合体类型与集合之间的转换过程中,可能会打破原本的顺序**
```
>>> l1 = ['1','2','3','4','5']
>>> sl1 = set(l1)

{'4', '1', '5', '2', '3'}
>>> l2 = list(sl1)
>>> l2
['4', '1', '5', '2', '3']
>>> 
```

## 12. bool

* python中有一个名为Bool的显示布尔数据类型， 内部 True 和 False 是该类型的实例，**而bool类型实际上只是内置整数类型的字类，True和False的行为与 0 和 1 是一样的。**

