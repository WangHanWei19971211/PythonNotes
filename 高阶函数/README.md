## 高阶函数

# 一、Python reduce() 函数

#### 模块简介

functools，用于高阶函数：指那些作用于函数或者返回其它函数的函数，通常只要是可以被当做函数调用的对象就是这个模块的目标。

### 描述

**reduce()** 函数会对参数序列中元素进行累积。

函数将一个数据集合（链表，元组等）中的所有数据进行下列操作：用传给 reduce 中的函数 function（有两个参数）先对集合中的第 1、2 个元素进行操作，得到的结果再与第三个数据用 function 函数运算，最后得到一个结果。

### 语法

reduce() 函数语法：

```
reduce(function, iterable[, initializer])
```

### 参数

- function -- 函数，有两个参数
- iterable -- 可迭代对象
- initializer -- 可选，初始参数

### 返回值

返回函数计算结果。

### 实例

以下实例展示了 reduce() 的使用方法：

例1
```python

import functools as fs
list1 = [i for i in range(5)]#0 1 2 3 4
def add(a,b):
    print(a,b)
    return a+b
print(fs.reduce(add,list1)) #10
# print(fs.reduce(lambda x, y: x+y, list1)  # 使用 lambda 匿名函数,功能相同，输出10
```
结果：
~~~sql
0 1
1 2
3 3
6 4
10
~~~
例2
```python
sentences = ['The Deep Learning textbook is a resource intended to help students and practitioners enter the field of machine learning in general and deep learning in particular. '] 
def count(x,y):
    print(x,y)
    return x+y.count('learning')
#word_count =fs.reduce(lambda a,x:a+x.count("learning"),sentences,0)
word_count = fs.reduce(count,sentences,0)
print(word_count)
#统计次数最方便的是：print(sentences[0].count('learning'))
```
结果：
~~~sql
0 The Deep Learning textbook is a resource intended to help students and practitioners enter the field of machine learning in general and deep learning in particular. 
2
~~~

**注意：**

在 Python3 中，reduce() 函数已经被从全局名字空间里移除了，它现在被放置在 functools 模块里，如果想要使用它，则需要通过引入 functools 模块来调用 reduce() 函数：

Python3 统计某字符串重复次数:

```python
from functools import reduce
sentences = ['The Deep Learning textbook is a resource intended to help students and practitioners enter the field of machine learning in general and deep learning in particular. '] 
word_count =reduce(lambda a,x:a+x.count("learning"),sentences,0)
print(word_count)
```

输出结果为：

```
2
```

当然，如果只是单纯实现功能可以使用以下方式：

```python
from functools import reduce

sentences = ['The Deep Learning textbook is a resource intended to help students and practitioners enter the field of machine learning in general and deep learning in particular. '] 
print(sentences[0].count('learning'))
```



# 二、Python map() 函数

#### 描述

**map()** 会根据提供的函数对指定序列做映射。

第一个参数 function 以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的新列表。

#### 语法

map() 函数语法：

```
map(function, iterable, ...)
```

#### 参数

- function -- 函数
- iterable -- 一个或多个序列

#### 返回值

Python 2.x 返回列表。

Python 3.x 返回迭代器。

#### 实例

以下实例展示了 map() 的使用方法：
例1:
```python
#计算平方数
list1 = [1,2,3,4]
def func(arg):
    return arg**2
print(map(func,list1))
print(list(map(func,list1)))
print(list(map(lambda x:x**2,list1)))
```
结果：
~~~sql
<map object at 0x000001B2E0758E80>
[1, 4, 9, 16]
[1, 4, 9, 16]
~~~
例2:两个列表中元素相加
```python
list1 = [1,2,3,4]
list2 = [2,2,4,4]
def func(arg):
    return arg**2
#print(map(func,list1))
#print(list(map(func,list1)))
print(list(map(lambda x,y:x+y,list1,list2)))
```
结果：
~~~sql
[3, 4, 7, 8]
~~~



# 三、Python filter() 函数

#### 描述

**filter()** 函数用于过滤序列，过滤掉不符合条件的元素，返回由符合条件元素组成的新列表。

该接收两个参数，第一个为函数，第二个为序列，序列的每个元素作为参数传递给函数进行判断，然后返回 True 或 False，最后将返回 True 的元素放到新列表中。

> **注意:** Pyhton2.7 返回列表，Python3.x 返回迭代器对象

以下是 filter() 方法的语法:

```
filter(function, iterable)
```

#### 参数

- function -- 判断函数。
- iterable -- 可迭代对象。

#### 返回值

返回列表。

------

#### 实例

以下展示了使用 filter 函数的实例：

#### 过滤出列表中的所有奇数：

```python
def is_odd(n):    
    return n % 2 == 1 
newlist = filter(is_odd, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
print(newlist)
```

输出结果 ：

```
[1, 3, 5, 7, 9]
```

#### 关于filter()方法, python3和python2有一点不同

Python2.x 中返回的是过滤后的列表, 而 Python3 中返回到是一个 filter 类。

filter 类实现了 __iter__ 和 __next__ 方法, 可以看成是一个迭代器, 有惰性运算的特性, 相对 Python2.x 提升了性能, 可以节约内存。

```python
a = filter(lambda x: x % 2 == 0, range(10))
print(a)
```



# 四、Python sorted() 函数

#### 描述

**sorted()** 函数对所有可迭代的对象进行排序操作。

> **sort 与 sorted 区别：**
>
> sort 是应用在 list 上的方法，sorted 可以对所有可迭代的对象进行排序操作。
>
> list 的 sort 方法返回的是对已经存在的列表进行操作，无返回值，而内建函数 sorted 方法返回的是一个新的 list，而不是在原来的基础上进行的操作。

#### 语法

sorted 语法：

```
sorted(iterable[, cmp[, key[, reverse]]])
```

参数说明：

- iterable -- 可迭代对象。
- cmp -- 比较的函数，这个具有两个参数，参数的值都是从可迭代对象中取出，此函数必须遵守的规则为，大于则返回1，小于则返回-1，等于则返回0。(cmp函数是python2中的 在python3中不存在了)
- key -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
- reverse -- 排序规则，reverse = True 降序 ， reverse = False 升序（默认）。

#### 返回值

返回重新排序的列表。

#### 实例

以下实例展示了 sorted 的使用方法：

```python
>>>a = [5,7,6,3,4,1,2]
>>> b = sorted(a)       # 保留原列表
>>> a 
[5, 7, 6, 3, 4, 1, 2]
>>> b
[1, 2, 3, 4, 5, 6, 7]
 
>>> L=[('b',2),('a',1),('c',3),('d',4)]
>>> sorted(L, cmp=lambda x,y:cmp(x[1],y[1]))   # 利用cmp函数
[('a', 1), ('b', 2), ('c', 3), ('d', 4)]
>>> sorted(L, key=lambda x:x[1])               # 利用key
[('a', 1), ('b', 2), ('c', 3), ('d', 4)]
 
 
>>> students = [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
>>> sorted(students, key=lambda s: s[2])            # 按年龄排序
[('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
 
>>> sorted(students, key=lambda s: s[2], reverse=True)       # 按降序
[('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
>>>
```



# 五、Python eval() 函数

### 描述

eval() 函数用来执行一个字符串表达式，并返回表达式的值。

### 语法

以下是 eval() 方法的语法:

```
eval(expression[, globals[, locals]])
```

### 参数

- expression -- 表达式。
- globals -- 变量作用域，全局命名空间，如果被提供，则必须是一个字典对象。
- locals -- 变量作用域，局部命名空间，如果被提供，可以是任何映射对象。

### 返回值

返回表达式计算结果。

------

## 实例

以下展示了使用 eval() 方法的实例：

```python
>>>x = 7
>>> eval( '3 * x' )
21
>>> eval('pow(2,2)')
4
>>> eval('2 + 2')
4
>>> n=81
>>> eval("n + 4")
85
```

第二和第三个参数的使用

```python
x = 10
def func():
    y = 20   #局部变量y
    a = eval("x+y")
    print("a:",a)      #x没有就调用全局变量
    b = eval("x+y",{"x":1,"y":2})     #定义局部变量，优先调用
    print("b:",b)
    c = eval("x+y",{"x":1,"y":2},{"y":3,"z":4})  
    print("c:",c)  
    d = eval("print(x,y)")
    print("d:",d)   #对于变量d，因为print()函数不是一个计算表达式，因此没有返回值
func()
```

**上课实例代码**

```python
x = 1
y = 2


def test_eval():
    # 查找了全局变量 3
    # print(eval('x+y'))
    # 添加局部变量 x y
    # x = 10
    # y = 20
    # 使用了局部变量
    # print(eval('x+y'))
    # 我想使用全局变量的 x y
    # print(eval('x+y',globals()))
    # 获取局部变量
    # print(eval('x+y',globals(),locals()))
    # print(eval('x+y',{'x':10,'y':20})) # 30
    print(eval('x+y',{'x':10,'y':20},{'x':2,'y':4}))
```



# 六、Python exec函数

**函数的作用：**

**动态执行python代码**。也就是说**exec可以执行复杂的python代码，而不像eval函数那样只能计算一个表达式的值。**

```
exec(source, globals=None, locals=None, /)
```

source：必选参数，表示需要被指定的python代码。它必须是字符串或code对象。如果source是一个字符串，该字符串会先被解析为一组python语句，然后执行。如果source是一个code对象，那么它只是被简单的执行。

**返回值：**

exec函数的返回值永远为None。

**eval()函数和exec()函数的区别：**

eval()函数只能计算单个表达式的值，而exec()函数可以动态运行代码段。

eval()函数可以有返回值，而exec()函数返回值永远为None。

**例1：**

我们把eval中的例子拿过来执行

```python
x = 10
def func():
    y = 20
    a = exec("x+y")
    print("a:",a)
    b = exec("x+y",{"x":1,"y":2})
    print("b:",b)
    c = exec("x+y",{"x":1,"y":2},{"y":3,"z":4})
    print("c:",c)
    d = exec("print(x,y)")
    print("d:",d)
func()
```

**执行结果：**

```python
#exec不会有任何返回值
a: None   
b: None
c: None
10 20
d: None
```

**例2**

```python
x = 10
expr = """
z = 30
sum = x + y + z   #一大包代码
print(sum)
"""
def func():
    y = 20
    exec(expr)   10+20+30
    exec(expr,{'x':1,'y':2}) 1+2+30
    exec(expr,{'x':1,'y':2},{'y':3,'z':4}) #1+3+30，x是定义全局变量1，y是局部变量

func()
```

执行结果：

```
60
33
34
```

##### 例3

```python
r = exec("for i in range(10): print(i)")
print(r)
```



# 七、Python complie函数

**函数的作用：**

```
compile(source, filename, mode, flags=0, dont_inherit=False, optimize=-1)
```

**参数说明**：

source：字符串或AST（抽像语法树）对象，表示需要进行编译的python代码

filename：指定需要编译的代码文件，如果不是文件读取代码则传递一些可辨认的值。

mode：用于标识必须当做那类代表来编译；如果source是由一个代码语句序列组成，则指定mode=‘exec’，如果source由单个表达式组成，则指定mode=‘eval’；如果source是由一个单独的交互式语句组成，则指定modo=‘single’。**必须要制定，不然肯定会报错。**

例子：

```python
s = """              #一大段代码
for x in range(10):
    print(x, end='')  
print()
"""
code_exec = compile(s, '<string>', 'exec')   #必须要指定mode，指定错了和不指定就会报错。
code_eval = compile('10 + 20', '<string>', 'eval')   #单个表达式
code_single = compile('name = input("Input Your Name: ")', '<string>', 'single')   #交互式

a = exec(code_exec)   使用的exec，因此没有返回值
b = eval(code_eval)  

c = exec(code_single)  交互
d = eval(code_single)

print('a: ', a)
print('b: ', b)
print('c: ', c)
print('name: ', name)
print('d: ', d)
print('name; ', name)
```

**执行结果：**

```python
0123456789  #有print就会打印
Input Your Name: kebi
Input Your Name: kebi
a:  None
b:  30
c:  None
name:  kebi
d:  None
name;  kebi
```
