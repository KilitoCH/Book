# Python!

## 怎么"hello world!"?
### Python中的字符串和变量和数据类型
***
在`Python`中既可以使用`' '`也可以使用`" "`来包含一个字符串。输出时直接使用
```python
print('Hello world!')
```
就可以了，没错既不需要写个package，也不需要一个class，甚至没有大括号和分号！！！
那么如果要输出一个叫`str`包含着`Hello world!`的变量咋整呢？
```python
str = 'Hello world!'
print(str)
```
还是，没有class，没有大括号，没有分号。等等，甚至没有  **`String`**，Amazing，啥都没有。没错Python是弱类型的，你不需要去定义一个变量的类型，只需要装点东西进去，Python就会知道他是什么类型，你还可以这样写：
```python
str = 'Hello world!'
str = 666
```
也就是说他甚至不像`var`这种只是不需要显示指定，甚至可以没得类型。
关于字符串还有一点需要注意，可以像是在C和Java中一样，Format一个字符串，但是语法稍有不同，`%d`,`%s`等等还是一样用，但是后面的变量应该使用`% ()`包含起来。例如：
```Python
str = 'Hello world!'
index = 1
print('Output times:%d.Content:%s' % (index,str))
```
需要注意的是在python中`and`,`or`,`not`都是关键字，用于逻辑运算，同时布尔值`True`和`False`必须要大写。

### Python里的list(集合)和tuple(一个不能变的list)
Python里头的list跟其他语言（比如Java）的差不太多，也是可以存不同类型的元素进去，定义的时候类似数组，可以索引（可以用`[]`的数组索引符号，这一点上是跟Java不太一样的），可以从尾部添加，也可以在任意索引处添加。它有一个很神奇的地方：可以从尾部索引，正常来说应该是：
```Python
str_list = ['Hello','world','!']
str_list[len(str_list) - 1]
```
但是在python里面可以用`str_list[-1]`来索引最后一个数！！！其他的依此类推。然后他有一些方法，如下表：
|function|comment|
|:-:|:-:|
|`append(arg)`|arg为要添加的元素，会被添加到集合末尾|
|`insert(index,arg)`|index为要插入的位置，arg为要添加的元素，arg会被添加到index指定的位置|
|`pop()`|类似于栈的语法，从集合末尾删除元素|
|`pop(index)`|删除index处的元素|
tuple就是一个固定的list，他的表元素一经定义就无法修改，他一样可以像数组一样被索引。但是如果你在tuple里面存储一个list，再去改list的内容是可以的。tuple的声明跟list一样，除了把`[]`换成`()`。
```python
#list:
alist = ['hello','world!']
#tuple:
atuple = ('hello','world!')
```
注：只有一个元素的tuple为了避免混淆数字1和只包含一个元素1的tuple类型，需要在声明这种tuple时在数字后加`,`,例如`atuple = (1,)`
用list写个Hello world！
```python
str_list = ['hello']
str_list.append('world!')
print(str_list[0],str_list[1])
```
### 逻辑控制语句
从前面看到的一些代码我看出来一个问题，在python中一个语句完了其实是不需要打`;`的！（惊人发现（
同时也没有大括号，这点跟`yaml`的语法倒是很像，可以说是很简洁了。所以python里的逻辑控制语句也稍微有些不一样，以`if`和`for`为例：
```python
if statement:
    run something
elif statement:
    run something
else
    run something

#这个for in 语法等效于foreach语法
for a in b
#python中没有其他语言那种for(i)的语法，只能用while，这跟别的一模一样
while statement：
    do something
```
在循环体中可以使用`break`和`continue`，功能跟其他语言一致。

### dict(字典)和set
这个dic跟Java里的map有一样的功能，用来存储键值对`<key,value>`,初始化的语法如下：
```python
dict = {'k1':v1,'k2':v2}
```
从字典中取值可以直接用键值作为参数检索。往一个已经存在的字典添加内容也很简单：`dict['k3']:v3`就可以添加一个新的值进去。对于dict有个关键字`in`可以用来检查dict里面是否包含某键值，不存在时会返回`False`，也可以用`get()`方法代替，区别在于不存在会返回`None`。删除时可以用`pop(key)`方法。
> 注意，key不能重复!且必须要是不可变类型。
set更像是数学意义上的集合，可以支持逻辑运算符，也不能存储重复键值，暂时没看到有啥用。

### 函数
首先，python没有大括号，本来想说括号爱好者有些许不满，但是他是以缩进来区分代码块的，爱了爱了。定义一个函数需要使用`def`关键字，不需要定义返回值，但是需要有参数集，要有最后面的`:`。由于没了大括号，python提供了一个新的关键字`pass`作为占位符，你可以写一个没有任何内容的函数，只包含一个pass语句，这个函数就没有任何功能。也可以把`pass`写在其他地方，比如`if`块里。举例：
```python
def my_function():
        pass
```
可以做类型检查，语法是`isinstance(val,(instance))`。函数可以返回多个值，其实是装在tuple里面，多个对应个数的参数可以直接接收这个tuple。

函数参数：有下列几种类型，对应着其他高级语言里面的重载或者可变参数。

#### 普通参数
就如同其他所有语言一样
```python
def my_function(par1,par2):
    pass
```
#### 默认参数
类似于重载，当给某个参数提供默认参数之后，不需要提供这个参数就可以调用函数。需要注意的是在python中想表达“空”这个意思的时候，需要用`None`而不是`Null`。
```python
def my_function(par1,par2 = 1):
    pass
#调用这个方法的时候可以只给par1不给par2，这时候就相当于你重载一个函数之后，把要的这个参数自己给值了
```
> **注意：**使用默认参数确实会产生一些问题，就是最好把默认参数指向一个不可变参数，如果指向一个可变参数的话，你写入之后这个参数的值就会发生改变，这样你下一次用这个默认参数的时候就会发现你得不到默认输出。

#### 可变参数
使用可变参数的意义是你可以把参数集作为一个list给进去，并且还不用预先规定list的大小。用的时候用`for in`来遍历你的参数表就可以了。
```python
def my_function(*numbers):
    pass
#调用这个方法可以直接用：
my_function(1,2,3)
#如果你已经有一个list了，可以这样：
my_list = [1,2,3,4]
my_function(*my_list)
```

#### 关键字参数
第一种调用的方法其实就会和可变参数一样，区别在于声明方法为:
```python
def my_function(**args):
    pass
```
这里args在方法内会被自动包装成一个字典，所以传入的时候我们同样可以传入一个字典，方法同上述可变参数，区别在于要用两个`**`。同时也可以直接用定义字典的写法传入参数。用关键字参数还可以使用“命名关键字参数”，函数的定义如下：
```python
#如果这里*后面不跟任何内容，arg1和arg2就是字典的两个键值。
def my_function(*,arg1,arg2):
    pass
#如果*后面跟一个关键字，那么这就是一个可变参数，后续的是关键字参数，也不再需要使用*分隔
def my_function(*args,arg1,arg2):
    pass
#这里args就是可变参数，arg1和arg2是关键字参数的两个键值
```

## 一些高级特性
### 切片（暂时了解到的就类似于subString())
切片暂时唯一了解到的用法就是使用在list里面，用法举例：
```python
alist = ['hello','world']
print(alist[1:2])
#当起始位置是1时，可以写成：
###
#严重存疑，尝试的时候发现后一个数字指的确实是第几个，前一个数字的意义并不很明确，可以查一下手册，至少空着不写一定是从头开始没错
###
print(alist[:2])
#注意这里的3并非指下标为3的元素，而是第三个！除此之外还可以倒着取，效果也是一样的。
#还可以再加一个冒号指定每几个取一个
print(alist[:2:2])
#对字符串也可以这样操作
astr = 'Hello world!'
print(astr[:5])
#输出Hello
```
### 迭代
类似于foreach，一般在Java中这是用来遍历集合或者字典的，一样的在python里面也能这么遍历，但是同时也可以用来遍历其他的可迭代的对象。对字典的遍历语法：
```python
adict = {'a': 1, 'b': 2, 'c': 3}
#遍历键值
for key in adict:
    pass
#遍历数值
for value in adict.values():
    pass
#遍历键值对
for k,v in adict.items():
    pass
```
要判断一个对象是否是可迭代的，可以判断其是否是一个Iterable类型：
```python
from collections import Iterable

alist = [1,2,3]

print(isinstance(alist,Iterable))

```
python内置的`enumerate()`方法可以把一个list变成一个索引元素对，这样可以在for循环中同时迭代索引和元素：
```python
alist = [1,2,3]

for i,val in enumerate(alist):
    pass
```
### 生成器
用来生成一个序列，但是区别在于不是直接返回一个计算好了的序列，而是给出一个计算的逻辑，当你用`next()`请求的时候才会返回下一个。举个例子，从返回一个序列到给出一个计算逻辑：
```python
#下面这个方法调用的时候在n < 100的时候会打印所有的n，大于等于100就完全退出
def get_number_list():
    n = 0
    while(n < 100):
        print(n)
        n = n + 1
    return 'done'
```
但是如果我不需要一次性得到所有的n，我该怎么办嘞，可以把`print`改成`yield`，这样函数运行到yiled的时候就会停住并且给出yield的表达式值，直到你调用next()的时候再取得下一个数：
```python
def get_number_list():
    n = 0
    while(n < 100):
        yield(n)
        n = n + 1
    return 'done'
```
这样你可以用`isinstance(get_number_list,Iterator)`来发现他是一个Iterator对象，实际上它是一个generator对象，这应该是子类和超类的关系。所以这个也可以用list()方法来产生一个集合。

### list生成式
这个用到时候再写吧……花里胡哨
贴一块源码：
```python
alist_1 = [x * x for x in range(1, 11)]

alist_2 = [x * x for x in range(1, 11) if x % 2 == 0]

alist_3 = [m + n for m in 'ABC' for n in 'XYZ']
```
### 迭代器
iter()方法，用这个方法作用于Iterable对象可以把他变成Iterator对象，区别在于Iterable对象不能用next()方法取下一个。

### 函数重载
python作为动态语言，想传递什么类型的参数就传递什么，但是python3中提供了一个注解帮助限制参数类型，语法如下：
```python
def func(argv: [Type]):
    pass
```
这样的语法能够限制argv必须是指定的`[Type]`类型，否则就会在运行时抛出类型异常，这就相当于对参数类型进行了严格限制。但是原本python是动态类型的，原本传什么类型都可以，现在只能传一种，这就产生了很大的限制。这就产生了重载的问题。
python对于重载给出了解决的办法，在python3.5之前，引入`Typing`包之后重载函数。在Python3.5之后`typing`已经成为了标准库的一部分，直接import就可。重载有两种方案：
* 使用`typing.TypeVar`。这个可以解决参数个数不变，只需要更改参数类型的情况。参考代码如下：
    ```python
    import typing

    T = typing.TypeVar('T',int,float,str)

    def foo(name: T):
        pass
    ```
    这样`name`就可以接收三个类型的参数，实现了函数的重载。
* 使用`typing.overload`，顾名思义，这就是函数的重载。使用时作为一个装饰符。
    ```python
    import typing

    @typing.overload
    def foo(name: str):
        pass
    
    @typing.overload
    def foo(name: float):
        pass
    
    def foo(name,age = 24):
        do something
    ```
    初看非常惊喜（其实没啥用，还不如就写一个再检查……，而且python用list、map作为参数，真的需要这么花哨的玩意吗），后来才发现这玩意完全没用，就是欺骗代码检查工具的！！！最后这个没有装饰器的函数会覆盖上面所有的，只有他才是有用的。

## 函数式编程
首先，python中有个很好的东西，函数可以作为变量传到别的函数或者变量里头。这个其实有点像Lambda表达式（这不废话，因为lambda表达式就是函数式编程的内容啊！！！）举个栗子：
```python
def my_function():
    return abs(1)

def my_another_function(f):
    return f()

print(my_another_function(my_function))
#其实如果是用这种已经定义好的方法，还可以有更牛批的
my_function = abs

def my_another_function(f):
    return f()

print(my_another_function(my_function))
#这想表达的是，太牛逼了，my_function通过这种方式，代表了abs函数！！！你就跟用abs一样用my_function就行了
```
**下面说点python设计好了的给你用的高级函数**
***
### map/reduce
map函数其实解决了一个还是看起来蛮有用的问题，就是如果你希望对一组变量执行同样的动作，那么你可能需要遍历循环一个作为参数表的`list`并且分别调用这个函数，然后再把所有的输出结果给拼起来。
python提供了这么一种方法，叫做`map`。调用如下：
```python
alist = [1,2,3,4,5,6,7,8]

print(map(abs,alist))
```
这就是map的用法，给个list，对list里头的每个值都取绝对值然后返回一个Iterator。但是这里有个问题，因为返回的是一个Iterator，有点像是一个生成器，这个打印会得到：`<map object at 0x7ff4e7565370>`告诉你打印了一个对象。如果想看到一个list的输出，需要用`list()`函数计算并返回。上面的代码可以改成：
```python
alist = [1,2,3,4,5,6,7,8]

print(list(map(abs,alist)))
```
reduce方法看起来就没有那么有用了，贴个[链接](https://www.liaoxuefeng.com/wiki/1016959663602400/1017329367486080)，用得上的时候再说吧。

### filter（过滤器，暂时不用）

### sorted()函数
这个函数是用来进行临时排序，不会实际改变排序的序列。用法如下：
```python
alist = [9,2,5,2,1,6]

print(sorted(alist))
#这样就会输出排序之后的一个列表
```
除了上述用法之外，还可以再传入另外一个函数参数，排序之前会先用这个函数参数对列表中的所有元素做一遍操作再进行排序：
```python
alist = [9,2,-5,2,-1,6]

print(sorted(alist,key=abs))
#也就是说这里的key应该是一个关键字参数
#这里的绝对值的意思是排序之前的依据的时候会根据取绝对值之后的序列，但之后输出的仍是没有绝对值前的序列
```
### 返回函数和闭包
前面已经看到了函数可以作为参数被赋给一个变量，那么自然可以想到应该可以把函数作为变量返回。比如：
```python
def sum_all(i):
    val = 0
    def f():
        val = i + 1
        return val
    return f
#这样如果调用sum_all
function = sum_all
#上面这行语句是有问题的，需要注意的是sum_all指向的是一个函数的存放地点，是一个变量，可以看作指针，这里function指向的是sum_all的引用，所以要让function得到sum_all的返回值，就需要用
function = sum_all(1)
#会发现function指向了f！
#但是结果并不会被计算出来，还需要再调用f()才会完成计算
function()
```
闭包：上面这个用法其实就是闭包，我们只是在一开始写`function = sum_all(1)`的时候把这个参数给进去了，但是在我们调用`function()`之前，这个参数并没有被用于计算。这样就相当于这个变量被封闭起来了。
> 这里会带来另一个变量上的问题，如果自己实际遇到了再回来补充。

### 匿名函数：lambda表达式
这个从定义上看起来很简单，就是一个语法：
```python
lambda x: x + 1
这个可以直接等效成为下面的这个函数：
def my_function(x):
    return x + 1
```
也就是说在使用了lambda关键字之后，后面跟的是自变量，再后面跟的是返回值。不需要定义函数的名称。
当然lambda表达式定义出来的函数也可以被赋值给别的变量，然后用别的变量来调用：`f = lambda x: x + 1`。然后用`f(1)`调用。

### 装饰器
这个东西吧，我暂时觉得是为了让代码好看，简洁。或者说是在改代码的时候可以少改点，直接作为注解加到需要增加功能的方法上就行了，不需要很麻烦的再单独修改每个方法的实现。
那么什么是装饰器呢？其实就像装修，原来的房子已经有了，装修就是让房子变得更好看，更多功能。装饰器的执行过程就是把函数作为“装饰器”这个函数的参数传进去，看个例子：
```python
def log(func):
    def wrapper(*arg,**kwarg):
        print('Call:%s' % func.__name__)
        return func(*arg,*kwarg)
    return wrapper

@log
def foo(intVal):
    print(intVal)
```
分析上面这个例子，这个log函数就是一个装饰器，他包含一个叫wrapper的方法，为什么叫装饰器的精髓就在这了。
1. 先不管这个注解是怎么工作的，我们关心一下这个`wrapper(*arg,**kwarg)`方法，你会看到他**返回了传入了参数集的func()的结果**，这意味着什么呢，这意味着 **`wrapper()`取代了`func()`**，我们调用`wrapper()`等同于调用`func()`
2. 然后再看`log()`方法返回了啥，惊了，他返回了一个wrapper！！！注意，返回的不是`wrapper()`，而是`wrapper`。也就是说他返回了一个函数，而不是一个结果，那么等于说这么操作之后，就只是相当于在func执行前多执行了一句`print('Call:%s' % func.__name__)`，然后把他打包成新的方法返回给你。
3. 2之后，我们就会发现，加了这个注解，相当于是执行了这么一个语句：`foo = log(foo)`。那么问题就来了，这样注解之后，foo就不再是他自己了，他变成了wrapper!这时候再去查看foo的类型，会发现控制台打印：`<function log.<locals>.wrapper at 0x000001DBD1013310>`。foo被夺舍了，他不再是自己了。就好像我们直接执行了语句`foo = wrapper`一样。
4. 那么有没有什么方法让foo还是他自己呢，一种想法是把原本的信息都写给`wrapper`，这有点暴力难写。python提供了一个方法：在wrapper前面加个注解：`functools.wraps(arg)`，这里面的`arg`就是要把wrapper包装成的函数，在本例中就是被“夺舍”的foo,代码如下：
    ```python
    import functools

    def log(func):
        @functools.wraps(foo)
        def wrapper(*arg,**kwarg):
            print('Call:%s' % func.__name__)
            return func(*arg,*kwarg)
    return wrapper
    ```
    执行之后再看foo的类型，结果：`<function foo at 0x000001F117FD3310>`。Amazing！！！foo又回来了。

上述装饰器其实已经非常的amazing了，但是这有个问题，log也没法接收别的参数，每个需要装饰的方法都只能执行一样的动作，没法做出区分。为了能够给每个使用装饰器的方法再传点参数，需要用到如下语法：
```python
import functools

def decorator(val: str):
    print(val)
    def log(func):
        @functools.wraps(foo)
        def wrapper(*arg,**kwarg):
            print('Call:%s' % func.__name__)
            return func(*arg,*kwarg)
    return wrapper
return log

@decorator('Hello decorator')
def foo():
    pass
```
这样整了之后会发现decorator这个注解也可以带参数了，这样写等效于：`foo = decorator(val)(foo)`，也就是说拿到参数之后decorator就变成了log了，最后跟上述装饰器本质上没啥区别，只是一种语法糖而已。


在这个部分学到一个很有用的知识：每个函数都有一个`__name__`变量，可以用来看一个变量装的到底是什么函数。(lambda函数赋值之后，打印会看到函数名为`<lambda>`)

### 偏函数
当函数的参数个数太多，需要简化时，使用functools.partial可以创建一个新的函数，这个新函数可以固定住原函数的部分参数，从而在调用时更简单。

## python里面的包
python里面的包其实跟其他语言（比如Java）里面的包是差不多的，在Java里头，导入一个Jar包之后，就可以通过import来导入需要的类。在python中也是一样，可以导入不同的python文件(称为module)然后就可以用模块里面的方法。

### 包的结构
python的package跟Jar包的结构是一样的，但是有个最大的区别，就是需要作为python包的目录下面必须要包含着一个`__init.py__`的文件，可以不包含内容，但是如果没有这个文件，python则不会把这个文件夹识别成一个包。
在调用的时候也跟Java的差不多，按照层级调用就可以。

### 使用一个包
* 在一个模块里面，第一个字符串（不加任何修饰的）会被看成是模块的说明注释。
* `sys`包，python内含的sys包允许你使用从命令行接受的参数，存储在名为`argv`的list里面，argv中变量的数量永远大于等于1，因为他有一个默认的参数为模块名。
* 在单独执行一个模块时，会有一个变量`__name__`被设置为`__main__`，所以我们可以设置一个判断：
```python
if __name__ == '__main__':
    function()
#就是说当__name__字段的值是'__main__'的时候才执行这个function方法，所以如果在别的地方调用这个模块，这个语句就不会被执行。
#那么理所当然也可以用这种方式来指定启动项？
```
* 前缀中加入了`_`或者`__`的函数或变量是非公开的（类似Java里面的private），不能被直接引用。
