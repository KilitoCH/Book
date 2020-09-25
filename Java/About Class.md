# 关于类
## Abstract修饰符
***
* 当给类标记Abstract后，这个类就不能被实例化（更像接口）
* 给方法标记Abstract后，这个方法不能有任何的实现内容（也不能包含大括号）
* 当继承一个Abstract类之后，必须将这个子类也标记为Abstract或实现超类中的所有Abstract方法；如果超类中实现了无参的构造函数，那么调用子类的构造函数时将自动调用这个超类无参构造函数；如果超类中没有任何无参构造函数，必须手动用`super`指定超类的带参数的构造器，否则编译器会给出一个错误。
## equals方法
***
| 应该避免只使用instanceof | 这个关键字用于检测一个`object_0`是否和另一个`object_1`是相同的类，但是问题在于当`object_0`是`object_1`的子类时，这个仍然会成立（反之则不会成立）。这会导致检测当实际上他们是继承而非相等关系时，得到`true`的结果。 |
|     :-:    |:-:|
|   自反性 | `a.equals(b)`与`b.equals(a)`应该得到相同的结果   |
|   非空性  |   对任意非空引用`x`，`x.equals(null)`应该返回`false`  |
***
### 设计建议
1. 显式参数命名为`otherObject`，并在稍后将其强制类型转换。
2. 检测`this`与`otherObjects`是否**指向了同一个对象引用**，若是，直接返回`true`:  
   `if (this == otherObjects)   return true;`  
3. 检测`otherObject`是否为`null`。  
   `if (oyherObject == null)    return false;`
4. 比较`this`和`otherObject`是否为同一个类。若不是，直接返回`false`。使用`getClass()`检测：  
   `if (this.getClass() != otherObject.getClass())  return false;`  
   **注意：**如果认可所有子类都可以互相比较，那么应该使用`instanceof`关键字来实现只要继承自同一个超类都得到`true`。  
   `if (!(otherObject instanceof ClassName))    return false;`
5. 使用强制类型转换将`otheObject`转换为当前的类型。注意如果在4中使用`instanceof`则应该将子类装入超类中。
6. 现在`otherObject`不是`null`，与当前的没有指向同一个引用且是一样的类，所以应该具体比较他们的字段是不是全部相等。对于基本类型可以使用`==`，对于其他使用`Object.equals`比较。
7. 如果在子类中实现`equals`方法，应该包含对超类的方法调用`super.equals(otherObjects)`，对子类无法直接访问（可以通过getter访问）的字段完成比较。


