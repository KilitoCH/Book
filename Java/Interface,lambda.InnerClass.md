# Interface&lambda&InnerClass
## Interface
***
* 接口中的方法自动声明为`public`，静态常量自动定义为`public static final`。接口中不允许定义变量字段。上述修饰符不用显式指定。
* 从**Java11**开始，接口中可以定义静态方法（静态方法不能被重写！但是可以在子类中定义重名方法实现多态，这里虽然重名但是没有覆盖。）
* 可以为接口提供默认实现，但必须用`default`修饰符。
```
//example,这样继承这个接口的类不一定要实现方法
public interface Comparable<T>
{
    default int comparrTo(T other){ return 0;   }
}
```
* 在修改接口时这个就显得有意义了，否则所有`implements`这个接口的类都会报错，因为他们有没有实现的方法。这样提供一个默认方法的作用就体现出来了。
* 如果`extends`的超类和`implements`的接口定义了同一个方法，会默认考虑超类方法，接口的默认方法则会被忽略。
## 回调
***
### 需要引入的包：
```
import java.awt.event.*;
```
这有些类似于函数变量。但是不同的是这里不能把方法名作为变量，而是只能以一个对象（一个实例）作为参数传入。
这些类需要实现一个只包含有一个方法的接口，这样这个对象就会被当作这个方法的入口。
## 对象克隆
***
**重点：实现`Cloneable`接口**
若只是简单的赋值操作如：
```
var original = new AClass();
AClass copy = original;
```
这里的`original`和`copy`会引用同一个对象，任何修改操作都会同时修改这两份引用。
### 浅拷贝
只拷贝数值或者其他基本类型，对于子对象 会创建对同一个对象的引用。
> 注：浅拷贝在某些时候也是安全的，比如没有子对象，只有数值或者其他基本类型；再比如所有的子对象都是安全的，即对象的内容已经无法更改，这时即便所有副本引用同一个对象也没关系。
### 深拷贝
不仅拷贝数值和其他基本类型，也同时克隆所有的子对象。
> 这就像一个嵌套，要完成深拷贝，必须所有子对象都只有数值和其他基本类型，这样我们可以调用Object.Clone()来实现子对象拷贝；或者所有子对象都实现Cloneable接口，以此类推。
### Example
```
//先调用Object类的Clone()方法实现浅拷贝，再调用子对象的Clone()方法实现深拷贝
Class Employee implements Cloneable
{
    public Employee clone() throws CloneNotSupportException
    {
        //call object clone
        Employee cloned = (Employee)super.Clone();

        //clone mutable fields
        cloned.hireDay = (Date)hireDay.Clone();

        return cloned;
    }
}
```
## lambda
***
lambda表达式是一个代码块，如：
```
(String first,String second)
    ->  first.length() - second.length()
```
* 如果无法用一个语句完成方法描述，则应将`->`后的代码放在`{}`中。
* 若lambda表达式无参数，仍要提供空括号。
* `{}`中的内容可以看作是一个方法，前面的括号则是参数集，这整个看起来就像是省略了方法名的方法。
> 说明：对于只有一个抽象方法的接口，需要这些接口的对象时就可以提供一个lambda表达式，这种接口称为函数式接口(functional interface)，也可将lambda表达式整个保存到函数式接口中。
### 方法引用
例如
```
var timer = new Timer(1000,event -> System.out.println(event));
//可简化为：
var timer = new Timer(1000,System.out::println);
```
只有当lambda表达式只调用一个方法而不做其他操作时才能把lambda表达式重写为方法引用，主要有以下三种情况：
1. `object::instanceMethod`
   > 即把`object`作为参数传递给方法。
2. `Class::instanceMethod`
   > 第一个参数会作为方法的隐式参数，第二个参数则会作为显式参数。
3. `Class::staticMethod`
   > 所有参数依次传递到静态方法，因为静态方法不需要隐式参数，所以全部作为显式参数。
### lambda表达式中的变量
除了显式参数之外，lambda表达式可以访问外围方法或者类中的变量，lambda表达式会对这些变量进行存储。也正因如此，需要注意的是在lambda表达式中，只能引用“值不会改变的变量”，即lambda表达式中捕获的变量必须是实际上的[事实最终变量]，即被捕获之后它无论在代码块内还是快外都不会再改变了。