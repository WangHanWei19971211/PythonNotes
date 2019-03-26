# 日期和时间

## 一 time模块

##### import time

时间的表示形式：

##### 时间戳	时间戳是指格林威治时间1970年01月01日00时00分00秒(北京时间1970年01月01日08时00分00秒)起至现在的总秒数。



以整型或浮点型表示时间的一个以秒为单位的时间间隔。这个时间间隔的基础值是从1970年1月1日开始算起

## （一） 格式化日期的函数

| time.time()                              | 当前时间戳(秒数)   UNIX和Windows只支持到2038年。       |
| :--------------------------------------- | ---------------------------------------- |
| time.localtime()                         | 接收时间辍（1970纪元后经过的浮点秒数）并返回当地时间下的时间元组    (0是周一) |
| time.strftime("%Y-%m-%d %H:%M:%S"[,time.localtime()]) | 格式化成2016-03-20 11:45:39形式 第二个参数可有可无      |
| time.asctime()                           | 返回格式化后的英文文本的时间                           |
| time.mktime(tupletime)                   | 接受时间元组并返回时间辍                             |
| time.sleep(secs)                         | 推迟调用线程的运行，secs指秒数。                       |
| time.clock()                             | 用以浮点数计算的秒数返回当前的CPU时间。用来衡量不同程序的耗时，比time.time()更有用。 |
| time.strptime(“2013-10-10 23:40:00”, "%Y-%m-%d %H:%M:%S") | 将其转换为时间元组                                |

#### mktime的例子

```python
import time

t = (2016, 2, 17, 17, 3, 38, 1, 48, 0)
secs = time.mktime( t )
print ("time.mktime(t) : %f" %  secs)#time.mktime(t) : 1455699818.000000

time.strptime(“2013-10-10 23:40:00”, "%Y-%m-%d %H:%M:%S")

time = time.mktime(time.strptime("2013-10-10 23:40:00", "%Y-%m-%d %H:%M:%S"))
print(time.strftime("%Y-%m-%d %H:%M:%S",time.localtime(time)))
```

#### 计算程序运行的时间

```python
import time

def procedure():
    for i in range(10000):
       pass

# time.clock
t0 = time.clock()
procedure()
print (time.clock() - t0)

# time.time
t0 = time.time()
procedure()
print (time.time() - t0)
```

### （二） python中时间日期格式化符号

| %Y   | 4位的年                 | %y   | 2位的年                        |
| ---- | -------------------- | ---- | --------------------------- |
| %m   | 月份（01-12）            | %d   | 月内中的一天（0-31）                |
| %H   | 24小时制小时数（0-23）       | %I   | 12小时制小时数（01-12）             |
| %M   | 分钟数（00=59）           | %S   | 秒（00-59）                    |
| %a   | 本地简化星期名称 英文文本 简化     | %A   | c本地简化星期名称 英文文本 完整           |
| %j   | 年内的一天（001-366）       | %w   | 星期（0-6），星期天为星期的开始    (0是周一) |
| %x   | 本地相应的日期表示 (08/02/17) | %X   | 本地相应的时间表示 23:48:34          |

**例子：**计算一个人活了多久

## 日历（Calendar）模块

**calendar.isleap(year)**
是闰年返回 True，否则为 false。

```python
import calendar
print(calendar.isleap(2000))
True
print(calendar.isleap(1900))
False
```

**calendar.leapdays(y1,y2)**
返回在Y1，Y2两年之间的闰年总数。

**calendar.month(year,month,w=2,l=1)**
返回一个多行字符串格式的year年month月日历，两行标题，一周一行。每日宽度间隔为w字符。每行的长度为7* w+6。l是每星期的行数。

##### 获取某月日历

```python
import calendar

cal = calendar.month(2016, 1)
print ("以下输出2016年1月份的日历:")
print (cal)

例子：Python 生成日历
# 引入日历模块
import calendar

# 输入指定年月
yy = int(input("输入年份: "))
mm = int(input("输入月份: "))

# 显示日历
print(calendar.month(yy,mm))
```



## 二 datetime模块

##### import datetime

datetime比time高级了不少，可以理解为datetime基于time进行了封装，提供了各位使用的函数，datetime模块的接口更直观，更容易调用

```python
from datetime import datetime
本地时间 datetime.now() #2017-08-03 00:13:00.690975
utc时间 datetime.utcnow()  

#获取指定时间
d2 = datetime.datetime(1999, 10, 1, 10, 28, 25, 123456) #年月日 时分秒 微妙数 1999-10-01 10:28:25.000001
#没有微妙数 省略
d2 = datetime.datetime(1999, 10, 1, 10, 28, 25) #1999-10-01 10:28:25
```

### datetime 转换成时间戳

把一个`datetime`类型转换为timestamp**['taɪmstæmp]**只需要简单调用`timestamp()`方法：

```python
>>> from datetime import datetime
>>> dt = datetime(2015, 4, 19, 12, 20) # 用指定日期时间创建datetime
>>> dt.timestamp() # 把datetime转换为timestamp
	datetime.now().timestamp()
1429417200.0
```

注意Python的timestamp是一个浮点数。如果有小数位，小数位表示毫秒数。

### timestamp转换为datetime

要把timestamp转换为`datetime`，使用`datetime`提供的`fromtimestamp()`方法：

```python
>>> from datetime import datetime
>>> t = 1429417200.0
>>> print(datetime.fromtimestamp(t))
2015-04-19 12:20:00
```

注意到timestamp是一个浮点数，它没有时区的概念，而datetime是有时区的。上述转换是在timestamp和本地时间做转换。

#### timestamp也可以直接被转换到UTC标准时区的时间：

```python
>>> from datetime import datetime
>>> t = 1429417200.0
>>> print(datetime.fromtimestamp(t)) # 本地时间
2015-04-19 12:20:00
>>> print(datetime.utcfromtimestamp(t)) # UTC时间
2015-04-19 04:20:00
```



### str转换为datetime

很多时候，用户输入的日期和时间是字符串，要处理日期和时间，首先必须把str转换为datetime。转换方法是通过`datetime.strptime()`实现，需要一个日期和时间的格式化字符串：

```Python
>>> from datetime import datetime
>>> cday = datetime.strptime('2015-6-1 18:19:59', '%Y-%m-%d %H:%M:%S')
>>> print(cday)s
2015-06-01 18:19:59
```

字符串`'%Y-%m-%d %H:%M:%S'`规定了日期和时间部分的格式。详细的说明请参考[Python文档](https://docs.python.org/3/library/datetime.html#strftime-strptime-behavior)。

注意转换后的datetime是没有时区信息的。

### datetime转换为str

如果已经有了datetime对象，要把它格式化为字符串显示给用户，就需要转换为str，转换方法是通过`strftime()`实现的，同样需要一个日期和时间的格式化字符串：

```python
>>> from datetime import datetime
>>> now = datetime.now()
>>> print(now.strftime('%a, %b %d %H:%M'))
Mon, May 05 16:28
```
#### Python 获取昨天日期

```python
# 引入 datetime 模块
import datetime
def getYesterday(): 
    today=datetime.date.today() 
    oneday=datetime.timedelta(days=1) 
    yesterday=today-oneday  
    return yesterday
 
# 输出
print(getYesterday())
```

