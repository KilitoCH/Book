# Introduction

## 重要部分
* Annotaion修饰符
* 测试工具
* 测试套件（可以将数个测试同时执行）
* 软件包：org.junit.*;

## 一些注意事项
* 测试方法必须使用 @Test 修饰
* 测试方法必须使用 public void 进行修饰，不能带参数
* 一般使用单元测试会新建一个 test 目录存放测试代码，在生产部署的时候只需要将 test 目录下代码删除即可
* 测试代码的包应该和被测试代码包结构保持一致
* 测试单元中的每个方法必须可以独立测试，方法间不能有任何依赖
* 测试类一般使用 Test 作为类名的后缀
* 测试方法使一般用 test 作为方法名的前缀

## 一些常用注解：
* @Test:将一个普通方法修饰成一个测试方法 @Test(excepted=xx.class): xx.class 表示异常类，表示测试的方法抛出此异常时，认为是正常的测试通过的 @Test(timeout = 毫秒数) :测试方法执行时间是否符合预期
* @BeforeClass： 会在所有的方法执行前被执行，static 方法 （全局只会执行一次，而且是第一个运行）
* @AfterClass：会在所有的方法执行之后进行执行，static 方法 （全局只会执行一次，而且是最后一个运行）
* @Before：会在每一个测试方法被运行前执行一次
* @After：会在每一个测试方法运行后被执行一次
* @Ignore：所修饰的测试方法会被测试运行器忽略
* @RunWith：可以更改测试运行器 org.junit.runner.Runner
Parameters：参数化注解

## 初次使用Junit
* 首先创建测试类，并应该在其中每一个`@Test`的方法中使用`assert`来检查结果。
* 创建`Test Runner`类，使用`Junit`的`JunitCore`类的`runClasses`方法执行上述测试类。可以获取到上述测试用例运行的结果。代码示例：
``` java
import org.junit.runner.JUnitCore;
import org.junit.runner.Result;
import org.junit.runner.notification.Failure;

public class TestRunner {
   public static void main(String[] args) {
      Result result = JUnitCore.runClasses(TestJunit.class);
      for (Failure failure : result.getFailures()) {
         System.out.println(failure.toString());
      }
      System.out.println(result.wasSuccessful());
   }
}   
```

## Junit中的重要API
***
### Assert类。
|              方法              |            描述            |
| :----------------------------: | :------------------------: |
| assertEquals(expected,actual)  | 检查两个变量或等式是否平衡 |
| assertFalse(boolean condition) |        检查条件为假        |
|  assertNotNull(Object object)  |      检查对象不是空的      |
|   assertNull(Object object)    |        检查对象为空        |
| assertTrue(boolean condition)  |        检测条件为真        |
***
### TestCase类
是一个abstract的类，提供了一些实用方法。可以强制有创建、拆除等动作。
***
### TestRunner类
可以批量运行输出一个类中所有标记了`@Test`方法的测试。
***
### TestResult 类
下面定义的是​`org.junit.TestResult`​类：
```
public class TestResult extends Object
```
​TestResult ​类收集所有执行测试案例的结果。它是收集参数层面的一个实例。这个实验框架区分失败和错误。失败是可以预料的并且可以通过假设来检查。错误是不可预料的。

### TestSuite类
* 通过使用注解@suite和注解@RunWith
* 通过TestSuite类我们可以同时运行许多的测试用例，下面这段代码即可说明：
```java
import junit.framework.*;
public class JunitTestSuite {
   public static void main(String[] a) {
      // add the test's in the suite
      TestSuite suite = new TestSuite(TestJunit1.class, TestJunit2.class, TestJunit3.class );
      TestResult result = new TestResult();
      suite.run(result);
      System.out.println("Number of test cases = " + result.runCount());
    }
}
```
这样我们可以把不同的测试用例写在不同的测试类里。

### Annotation
|  Annotation  |                               描述                                |
| :----------: | :---------------------------------------------------------------: |
|    @Test     |                      将这个方法作为测试案例                       |
| @BeforeClass |    在所有方法的前面运行,需要注意的是这个只在程序最开始运行一次    |
|   @Before    | 在@Test方法的前面运行，每个@Test方法执行之前都会执行@Before的方法 |
| @AfterClass  |     在所有方法的后面运行,需要注意的是这个只在程序最后运行一次     |
|    @After    | 在@Test方法的后面运行，每个@Test方法执行之后都会执行@After的方法  |

