# Reflect
首先应该引用两个类库  
```
import java.lang.reflect.*;
import java.util.*;
```
## Class
***
这里特指一个Java中提供的类，注意这里的**C**是大写的。
|   说明  | 对于任何一个类，使用`getClass()`方法都会返回一个`Class`类型的实例。`Class`对象会描述一个特定类的属性。  |
| :-: | :-: |
|   `getName()` |   得到这个类的类名，如果这个类放在一个包里，包的名字也将作为类名的一部分  |
|   `forName`   |   这是`Class`类的一个静态方法，会获得类名对应的`Class`对象    |
|   `getConstructor().newInstance()`   |    创建一个`Class`包含的对象的实例 |
|   `getModifiers()`    |   获得这个`Class`对象的构造函数的修饰符   |
|   `getFields()`    |   获得这个`Class`对象的字段   |
|   `getMethods()`    |   获得这个`Class`对象的的方法   |
|   `getConstructors()`    |   获得这个`Class`对象的构造函数的修饰符   |
## 异常申明
***
在使用Reflect时会出现一些检查型异常，例如在使用`Class.forName()`方法时，如果字符串指定的类不存在，就会抛出异常。我们应该认为设定异常和异常捕获代码。比如这里应该抛出`ReflectiveOperationException`。调用这个方法的任何方法也应该需要一个`throw`声明。
