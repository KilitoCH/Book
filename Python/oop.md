# 面向对象编程
## Class 定义
python中的类在用法上跟其他高级语言没有什么区别，也是定义一个`[包名][类名]`的结构。不一样的是在python中继承结构是在类名后面的括号中写继承的类，如果没有就写Object，所有的对象都应该继承自Object。
在类中有需要有一个初始化生成函数，在Java中这是一个跟类名一样，没有返回值的函数；但是在python中，需要定义一个名为`__init__`的函数。
python类中的字段**不需要预先定义**，用的时候再直接赋值就可以，所以在`__init__`中给`self.val`赋值了的变量就可以直接拿着用了。
上述代码如下：
```python
#定义类名和继承
class My_class(object):
    #定义构造函数，第一个参数必须是self
    #由于python弱类型，也不需要事先初始化变量，所以在__init__中赋值的变量也不需要在前面初始化了
    def __init__(self,*args):
    """
    python中的方法注释是写在两行三双引号中间
    """
        self.arg1 = arg1
        self.arg2 = arg2
...
#实例化上述类
#不需要new关键字，也不需要传入self，只需要传后面的几个参数就可以了
my_class = My_class(*args)
```
与其他任何oop的设计模式一样，变量可以有getter和setter方法，按照规范需要定义为`set_variable`和`get_variable`。

## 继承和多态
这部分跟Java的继承多态非常的像，被继承的称作超类或基类，继承后的称为子类。继承之后继承了超类的方法，你也可以直接用同名函数改写方法，这在Java和python中都被称为多态特性。
在多态上python与其他的高级语言有一个很大的不同点：对于别的语言来说，要把一个实例传入一个方法的时候，这个实例必须是这个对象或者是他的超类；对于Python则并非如此，传入的时候只要在里面调用的时候确实有这个方法就可以执行，不需要一定要是他的超类，这在python中被称为“鸭子类型”，也就是说它并不需要一定是一只鸭子，他只需要走起路来像个鸭子就行。这点非常有意思。(仔细一想，按照python的函数定义方式，好像它本身就没法限制要传入什么啊……)
有了继承之后，很自然我们就会需要判断一个变量/类的实际类型，有两种方法：
* `type()`方法
  `type()`方法可以用来判断对象的属性，返回值也可以用于比较两个对象是否是同一类型。我们也可以用`types`模块中定义的常量来判断对象的类型，即用type方法取得类型后与常量比较。
* `isinstance()`方法
  这个方法可以用来判断继承关系，除了前述的用法外，他还支持模糊判断，即一次与多个类型做比较，如果有一个正确就返回`True`。
  这里有一个非常有意思的小细节，看如下代码：
    ```python
    class ClassB(ClassA):
        pass

    print(isinstance(ClassB,ClassA))    
    ```
    上面应该会打印什么？看起来是要打印True，其实不是！！！ClassB确实是继承自ClassA，这个语句如果是用来判断他们俩是不是有继承关系，那肯定True。但是**ClassB的类型**并不是ClassB！！！它的类型是 **`Type`**!这里非常容易搞错，因为在别的高级语言中并不是这样的，应该用
    ```python
    print(isinstance(ClassB(),ClassA))
    ```
    我们看一下`isinstance(obj,class or tuple)`的参数表，第一个参数是一个对象，而不是一个类，所以你给一个ClassB的时候他会被看成一个对象，它还有自己的类型，需要构造一个实例，这个实例对象的类型才是ClassB。

除此之外，还可以用`dir()`方法来获得一个对象的所有属性和方法。还可以用`hasattr()`判断一个对象是否含有某个属性，等等。

> 一个小技巧，如同Java中的toString()方法，python中也有一些这样的推荐重载的函数，比如__len__()函数，重载这个之后，可以通过len()方法来调用这个内置方法。

## 实例属性和类属性
实例属性跟其他静态语言非常不一样，在Java中如果你定义了一个类，那么很显然，你的类有什么，实例就有什么，不可能再加了。但是在Java中就不一样了，除了类里面有的，实例自己居然还能往里塞。给一个实例的属性赋值的时候，如果类里面本来没有这个属性，那么属性将被创建。结合上述的dir()、getattr()、setattr()、hasattr()可以进行有效的属性管理。类似下面：
```python
class Aclass(object):

    def __init__(self,name):
        self.name = name

#下面这个是设定请求的属性
a_class = Aclass('a_class')
#下面就是自己瞎添加属性了
a_class.score = 100
#添加完了之后用hasattr()判断，发现确实是有这个属性了
```
类属性指的是跟Java等语言中的类一样的属性，每个实例都能访问到，都持有，但是在这里它更类似于一个全局变量，如果再给实例产生一个同名属性就会覆盖掉这个类属性。

## 动态绑定属性、方法
如同上面所说，在创建完实例之后我们还可以往里面添加属性。但是如果需要添加方法就需要用点不一样的语法：
```python
def a_function(self):
    #更神奇的是还能在这个方法里面再加属性……
    pass

from types import MethodType
#s是一个对象实例
s.a_function = MethodType(a_function,s)
```
那么这样乱加属性，迟早会出事，我们应该有一个机制能够对他们做出一些限制。比如使用`__slots__`属性。我们可以在类的`__slot__`属性中添加一个tuple来指定能动态添加的属性。指定之后，如果试图绑定没有指定的属性则会抛出异常。`__slot__`属性不会被自动继承，但是如果在子类中也设定这个属性，就会把超类的一块继承过来。

## 使用`@property`来简化getter和setter
正常定义一个私有变量的时候需要先有一个私有变量，然后有一个getter方法再有一个setter方法。写的时候倒也还好，但是在用的时候要分别调用getter和setter方法。那么`@property`可以简化这个操作，用法如下：
```python
class Aclass(object):
    #这里写一个返回一个属性的方法，本来一个正常的getter我们应该命名为get_score，而且需要在初始化的时候就有_socre属性
    #如果用@property就不一样了，直接用@property标记一个函数，就直接有了个属性还有了getter
    @property
    def score(self):
        return self._score

    #前面有了个@property之后，就会自动有一个attr.setter，我们再把它指定到一个函数
    @score.setter
    def score(self,value):
        self._socre = value
    #千万注意上一行里面不能写成self.score = value不然会死循环
    #上述这样标记之后，直接用socre就可以当正常属性一样用了，但是实际上分别调用了getter和setter
    
aclass = Aclass()
aclass.score(1)
```
没标记attr.setter的属性会变成只读属性。

## __call__方法
按照我的理解这就是给对象制定了一个默认方法，当你用实例名加括号调用的时候就会调用定义的`__call__`方法。我们还可以使用`callable`方法判断一个对象是否是可被调用的类实例。

## 枚举类
python的枚举有两个定义方法，首先你需要导入python提供的Enum类：`from enum import Enum`。然后使用Enum来初始化：
```python
from enum import Enum

Week = Enum('Week',('Mon','Tue','Wen','Thu','Fri','sat','sun'))
```
这就完成了定义一个枚举。可以直接使用Week.Mon来引用一个常量。也可以用`Week.__members__.items()`来查看一个枚举的所有值。相应的这样定义出来的枚举的每个常量会有一个值，默认从0开始编号。
我们还可以通过自己继承Enum类来创建枚举：
```python
from enum import Enum，unique

@unique
class Week(Enum):
    Sun = 0
    Mon = 1
    Tue = 2
    Wen = 3
    Thu = 4
    Fri = 5
    Sat = 6
```
这也能定义一个带值的枚举，@unique帮助检查有没有重复值。访问元素的方法：
```python
#通过直接访问元素
Week.Mon
#通过元素对应的值
Week[1]
#通过元素名
Week['Mon']
```

## 异常捕捉机制

### 基础使用
首先还是大家都有的try...catch...finally。python首先不一样的是关键字catch换成了except，直接写except后跟异常类型即可，这里还多了一点，catch后面finally前面还能加个else，看起来没啥用，但是这可以用来判断捕捉到异常了没，毕竟finally总会执行，但是else只有在没有捕捉到异常的时候才会执行。
```python
try:
    dosomething
except ExceptA as e:
    #这里e指的就是捕获到的异常的一个实例，因为异常也是一个类
    dosomething
except ExcepyB as e:
    dosomething
else:
    #如果一个异常都没捕捉到，就会进入这里的else代码块，这里跟别的语言不太一样
    dosomething
finally:
    dosomething
```
### 抛出异常
python中抛出异常用的关键字是raise，捕捉到的异常用关建字as，上述表述见如下代码：
```python
#在方法中抛出异常,可以抛出内嵌的异常，也可以自己定义异常（是一个类）,而且必须继承自BaseException，否则会在抛出和捕捉的语句分别触发异常。
class MyError(BaseException):
    pass

def my_function(s):
    n = int(s)
    if(n == 0):
        raise MyError('invalid value%s' % s)
    return 10 / n
#在上面这段代码中，如果n != 0，函数就会正常返回，但是如果命中，就会抛出异常，如果没有异常捕获机制程序就会立即中断。
#捕获这个异常的代码如下
def another_function():
    try:
        my_function('0')
    except MyError as e:
        print(e)
    else:
        print('没有捕获到异常')
    finally:
        print('End of function')
```
异常被`except`语句捕捉之后，可以在进行必要操作，比如打印错误信息之后不处理，原样抛出，写法如下：
```python
except Except as e:
    print(e)
    raise
```
即啥都不写，直接raise就代表原样抛出，等待他的调用者处理这个异常。
```python
except ExceptA as e:
    raise ExceptB()
```
就是说这个函数对异常有自己的理解，他觉得上面的异常不够准确，所以自己重新抛出了。最好是有实际关联的异常，否则可能导致后续程序没法处理。

### 异常栈
python中异常发生时会在控制台打印异常发生的调用层次，这跟Java是一致的。异常调用栈会从最外层的调用者开始，一层层剥开，直到最终找到到底是谁抛出了这个异常。这对于定位异常到底发生在哪是至关重要的，同时我们也需要注意调用栈意味着追踪了调用情况，那么我们就可以考虑在哪一层添加相对应的异常处理机制。

## python内嵌的调试方法

### print()
这个就不多谈，从C用到现在，已经烂熟于心了。指哪打哪，确实好用。

### 断言assert
这其实就是个带`break`的if else(?用法如下：
```python
assert n == 0,'n isn't zero'
```
就是验证n是不是等于0，如果是的话就没事，不是的话就抛出异常AssertionError，然后后面的字符串就是异常信息。
断言可以通过在运行时指定`-O`来关闭。

### logging
跟断言比，就是不会抛出异常导致程序退出，但是错误还是会被记录。用法如下：
```python
logging.info()
#或者debug,warning,error
```
运行之前需要指定logging的级别，只有对应级别的会生效，不指定就等于没有这些语句。
```python
import logging
logging.basicConfig(level = logging.INFO)
```

## 内嵌单元测试
写在前面，测试的时候可能会在模块里面进行输入测试，那么必须要注意的是请把测试的代码放在如下代码块后面：
```python
if __name__ == '__main__':
    unittest.main()
```
这样当不是要运行这个模块，而是调用模块的时候就不会错误调用之前用的一些测试方法了。

### 基本语法
跟Junit很像，写点不一样的点。
* 所有的测试函数需要放到一个测试类里面，测试类需要从`unittest.TestCase`继承。在测试类里面定义的函数需要用`test`开头，不以这个开头的不会被执行，可以用来做为辅助函数。
* 继承之后的类里面能看到许多断言，可以直接拿来做判断。
* 跟Junit的@After和@Before注解一样，可以写两个setUp和tearDown函数，分别会在测试前和测试后执行。

### 运行单元测试
* 第一种方式：
    ```python
    if __name__ == '__main__':
        unittest.main()
    ```
    然后可以跟运行任何文件一样运行。
    如果在IDE里面debug其实就无所谓了，比如在VS Code里面调试可以设定在当前模块启动。
* 第二种方式：在命令行加上`m unittest`，这样可以批量运行测试。

## 虚拟环境使用
[贴一篇virtualenv的教程](https://www.jianshu.com/p/a83a8f5d68dd?utm_campaign=maleskine&utm_content=note&utm_medium=writer_share&utm_source=weibo)