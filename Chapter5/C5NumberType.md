# Chapter5 Number

details about the Number type

## 整数与浮点数

### 整数

一般整数(32位)与长整数(无限精度)：当需要额外的精度时，整数会被自动转换成长整数 （Python2)

在Python3中， 只有整数一种类型，即上述两种已经被合并在一起了。

### 浮点数

浮点数带小数点，或者科学记数法的e或者E

在CPython中采用了C语言中的双精度来实现。

## 十六，八，二进制

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

### complex number(复数)

实部+虚部： 复数在技术上通过一对浮点数来实现，但是复数具有自己的一套运算法则

通过 `complex(real,imag)`来创建。