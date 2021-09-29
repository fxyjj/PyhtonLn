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

