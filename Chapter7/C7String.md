# String

Python 中的字符串类型

* 3.x: 
    1. str -> 用于Unicode文本，
    2. bytes -> 二进制文件
    3. bytearray -> bytes的可修改变体

## 1.字符串基础

### 1.1 python中没有为单个字符留有的字符类型，取而代之的是可以使用的单个字符的字符串
（C语言中有char 和 str类型，单个字符是新的char类型）

### 1.2 python中的字符串是不可变类型的，创建完成后字符串从左至右的顺序和每个位置上的信息都不可更改。

### 1.3 空字符串用一对里面不包含任何内容的引号（单引号或双引号）表示。

## 2.字符串操作基础

### 2.1 字符串操作

* concatenate(拼接): S1 + S2 （多态表现：操作符的意义由被操作的对象决定，此处加号操作字符串表示拼接，将两个字符串拼接在一起）
```
>>> s1 = 'Sean'
>>> s2 = ' Xiao'
>>> s1+s2
'Sean Xiao'
```

**注意在python中要用逗号将不同的字符串字面量分开，否则python会隐式将字符串拼接起来,添加逗号后即创建了一个元组**
```
>>> s1 = 'Sean' ' ' "Xiao"
>>> s1
'Sean Xiao'
>>> s1 = 'Sean',' ',"Xiao"
>>> s1
('Sean', ' ', 'Xiao')
```
*拼接不会改变被操作的字符串的顺序*

* duplication(重复): S1 * 3 (多态)
```
>>> s1 = 'a'
>>> s1 * 3
'aaa'
```

* index
```
>>> s1 = 'abcde'
>>> for i in range(len(s1)):
...     print(s1[i])
... 
a
b
c
d
e
```

* slice
```
>>> s1 = 'abcdefghijk'
>>> s1[1:2]
'b'
>>> s1[:2]
'ab'
>>> s1[0:]
'abcdefghijk'
>>> s1[1:]
'bcdefghijk'
>>> s1[1:-2]
'bcdefghi'
>>> s1[::-1]
'kjihgfedcba'
>>> s1[::2]
'acegik'
```

str[startIndex:endIndex(:step)]

分片有三个可选参数：

1. startIndex: 起始引索，表示开始分片的字符串引索， 默认为0，即第一个字符， 为正，表示从左至右引索，为负，则表示从右至左引索

2. endIndex: 结束引索，表示分片结束的字符串引索，莫认为len(str), 即最后一个字符串引索+1， 

3. step: 步长，表示分片时引索步长，默认为1， eg: step=2， 则挑选偶数index的元素； step=3，每隔两个元素挑选分片； step为负则表示从尾至首分片。 

**startIndex > endIndex, 否则分片为空，**
**分片区域为[startIndex,endIndex), 前开后和的区间**

*分片的规则与range(start,end ,step) 类似*

* 字符串格式化表达

1. %s

```
>>> s1 = 'SeanXiao'

>>> 'my Name is %s, Hello World!' % s1

'my Name is SeanXiao, Hello World!'

```

2. '{index1,index2,...}'.format(str1,str2,...)
```
>>> s1 = 'Dave'
>>> s2 = 'Stephie'
>>> s3 = 'Amy'
>>> S4 = 'Sam'

>>> '"{0} said he did his homework yesterday, so how about you,{2}?", {1} said to {3},"well, i plan to do it this afternoon!" {2} replied'.format(s1,s2,s3,S4)

'"Dave said he did his homework yesterday, so how about you,Amy?", Stephie said to Sam,"well, i plan to do it this afternoon!" Amy replied'
```

### 2.2 字符串字面量

* 引号

1. 单引号
```
'Sean',
'Sean said: "Hi,world!" '
```
2. 双引号
```
"Sean"
"Sean said: 'Hi, world!'"
```

3. 三引号
```
'''Multilines...'''
"""Multilines..."""
```
**Python 中单双引号是等价的，他们可以相互被包含使用，即'""' 表示字符串 ""; "''" 则表示 字符串 '' , 三引号可以允许我们键入换行符。**

* 转义字符，类似C语言转义字符，'\n','\t',等

* 原始字符串， 即取消转义功能`
```
>>> s1 = 'damn\nSean\t'
>>> s1
'damn\nSean\t'
>>> print('damn\nSean\t')
damn
Sean	
>>> print(r'damn\nSean\t')
damn\nSean\t
```
* 字节字面量(3.x and 2.6->) (more on future, 37 chapter)
b'sp\x01am'

* unicode字面量(more on later,37 chapter)
u'eggs\u0020sapm'

### 2.3 转义
一般用反斜杠(backslash) 来表示转义, 即引入特殊的字符编码，称为转义序列

* 字符\及其后面的一个或多个字符在生成字符串时会被单个字符所代替，
```
>>> s1='a\nb\tc'
>>> s1
'a\nb\tc'
>>> print(s1)
a
b	c
```
* P202 表7-2
* 空字符('\0') 不会结束一个字符串，而在python中会完整保留他的长度和文本。在python中没有字符可以结束一个字符串(C语言中有结尾字符eof)。
* python总是以16进制来显示转义字符，
```
>>> s = 's\tp\na\x00m'
>>> s
's\tp\na\x00m'
>>> print(s)
s   p
am
```
* 表7-2 最后一条表明，如果不是有效的转义字符，在python字符串中反斜杠会被保留而不会有转义的功能。
```
>>> s = 'C:\py\code'
>>> s
'C:\\py\\code'
>>> len(s)
10
>>> print(s)
C:\py\code
```
* 如果需要在字符串中编写反斜杠(`\`),那么需要使用(`\\`)额外的一个反斜杠来转义反斜杠，`\\` 是 `\` 的转义字符。
```
>>> s = 'C:\\py\\code'
>>> s
'C:\\py\\code'
>>> len(s)
10
>>> print(s)
C:\py\code
```
* 原始字符串阻止转义

*case*: 如果需要打开一个文件，其路径为：'C:\new\text.dat', 此时由于字符串包含反斜杠，所以python会将路径字符串中的\n 和 \t 转义位换行和制表符，所以会带来一些麻烦，

此时在字符串开头加上字母 r (小写或大写)， python会关闭转义机制，保留字符串中的反斜杠。
抑或是，如上所示，转义反斜杠，在字符串中的反斜杠前加上额外的一个反斜杠，此时python会保留反斜杠。实际上，当python在打印字符串时也是通过这种方式来显示反斜杠的。
```
>>> s = 'C:\new\text.dat'
>>> s
'C:\new\text.dat'
>>> print(s)
C:
ew  ext.dat

>>> s1 = r'C:\new\text.dat'
>>> s1
'C:\\new\\text.dat'
>>> print(s1)
C:\new\text.dat

>>> s2 = 'C:\\new\\text.dat'
>>> print(s2)
C:\new\text.dat
>>> s2
'C:\\new\\text.dat'

>>> s3 = r'C:\\new\\text.dat'
>>> s3
'C:\\\\new\\\\text.dat'
>>> print(s3)
C:\\new\\text.dat
>>> 
>>> len(s),len(s1),len(s2),len(s3)
(13, 15, 15, 17)
```
**注意在 Wins 和 UNIX 中 python会自动使用斜杠 '/' 来表示字符串路径，这是因为python试图以可移植的方式来解释路径。（所以上述路径在python中等价于'C:/new/text.dat'）**

* 原始字符串不能以奇数个反斜杠结束，因为若以反斜杠结束，它将会转义最后那个引号，而把他嵌入到字符串中，而这个操作对字符串来说不是有效的，所以需要注意。
```
>>> s = r'\'
  File "<stdin>", line 1
    s = r'\'
           ^
SyntaxError: EOL while scanning string literal
>>> s = r'\\'
>>> s = '\'
  File "<stdin>", line 1
    s = '\'
          ^
SyntaxError: EOL while scanning string literal
>>> s1 = '\\'
>>> s1
'\\'
>>> s2 = '\\\'
  File "<stdin>", line 1
    s2 = '\\\'
             ^
SyntaxError: EOL while scanning string literal
```
*如果需要以单个或者奇数个反斜杠结束字符串，我们可以采用分片slice,或者手动拼接，或者使用双反斜杠转义。*
```
# concatenate
>>> s = r'Sean'+'\\'
>>> s
'Sean\\'
>>> print(s)
Sean\

# slice
>>> s1 = r'Sean\\'[:-1]
>>> s1
'Sean\\'
>>> print(s1)
Sean\

#double back slash
>>> s2 = 'Sean\\'
>>> s2
'Sean\\'
>>> print(s)
Sean\
```
* 三引号的块字符串 (单双引号都可)

实际上python是在字符串折断处自动加上了换行符'\n',

**三引号可以用来注释掉一些暂时不用的大段代码，在没有特定IDLE支持下不能通过快捷键快速在每行前加上和删除掉#时，尤为如此。**



