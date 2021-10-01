# Chapter5 Number

details about the Number type

## 1. 数字类型

### 1.1 整数

一般整数(32位)与长整数(无限精度)：当需要额外的精度时，整数会被自动转换成长整数 （Python2)

在Python3中， 只有整数一种类型，即上述两种已经被合并在一起了。

### 1.2 浮点数

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

**需要注意的是， 浮点数的比较不总是会符合语气，如, 
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

