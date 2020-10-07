# 如何创建第一个Selenium工程
## 参考资料
如果你是对Selenium和WebDriver毫无了解，可以先查看Selenium给出的参考文档，虽然算不上非常详细，但是可以了解Selenium是怎么实现自动化测试工作的。[Selenium文档](https://www.selenium.dev/documentation/zh-cn/)
***
## 运行前准备
首先需要安装针对你浏览器的WebDriver和Selenium WebDriver
### 以ChromeDriver为例
进入[下载页面](https://sites.google.com/a/chromium.org/chromedriver/downloads)（Google的页面，如果打不开可以附邮箱我发给你）,按照自己的Chrome版本下载对应的驱动，可以在页面`chrome://settings/help`知道自己的Chrome版本。下载好之后不需要安装，将其中的exe文件解压到一个纯英文目录下，并将这个目录添加到`Path`中。<sup>[注1]</sup>
>如果这一步成功了，可以重新打开一个cmd窗口输入`chromedriver`查看是否成功启动。
### 在maven项目中导入相关的jar包
这里推荐使用阿里云的镜像Maven仓库，还提供了一个查询需要的包的页面。[阿里云云效Maven](https://maven.aliyun.com/mvn/search)，如果发现当前版本无法运行，可以检索其他版本的使用。  
要成功运行代码至少要添加`Java`的`Selenium`库，教程中给出了pom.xml的依赖项，但是阿里云仓库中找不到，我使用了如下替代：
``` java
<dependency>
    <groupId>com.applitools</groupId>
    <artifactId>eyes-selenium-java3</artifactId>
    <version>3.9</version>
    <type>pom</type>
</dependency>
```  
添加这个库之后你可以针对所有的浏览器进行自动化测试工作。如果你只需要对`Chrome`进行，可以导入：
``` java
<dependency>
    <groupId>org.seleniumhq.selenium</groupId>
    <artifactId>selenium-chrome-driver</artifactId>
    <version>4.0.0-alpha-6</version>
</dependency>
```
> 注意！经过测试，必须导入最新版本的包才可正常通过编译，如果你出现编译问题，替换版本为上述两个应该可以解决。
## 测试代码
### 初次运行
``` java
//首先应该在工程中导入WebDriver的类
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

//创建程序入口。你也可以使用Junit或者TestNG进行模块测试
public class Main {

    public static void main(String[] args)
    {
        //首先创建一个ChromeDriver的实例，这个实例用于模拟人和浏览器交互
        WebDriver driver = new ChromeDriver();
        //get方法用于导航到指定的url
        driver.get("https://www.baidu.com");
        //关闭浏览器并释放所有资源
        driver.quit();
    }

}
```
这段代码将首先开启一个新的浏览器，然后在浏览器刚刚加载完毕百度的页面时关闭浏览器结束程序。如果这段代码执行正常那么说明你的配置是完全正确的。如果最上面的ChromeDriver没有成功添加到环境变量中，在代码中也可以手动指定驱动地址：
``` java
//后一个参数应该填写解压出来的chromedriver所在的绝对路径
System.setProperty("webdriver.chrome.driver", "/path/to/chromedriver");
```
### 简单的Demo，在百度中搜索并截图保存搜索界面
``` java
//首先应该在工程中导入所需的类
import org.apache.commons.io.FileUtils;
import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

import java.io.File;
import java.io.IOException;
import java.time.Duration;

//创建程序入口。你也可以使用Junit或者TestNG进行模块测试
public class Main {

    public static void main(String[] args)
    {
        //首先创建一个ChromeDriver的实例，这个实例用于模拟人和浏览器交互
        WebDriver driver = new ChromeDriver();
        //get方法用于导航到指定的url
        driver.get("https://cn.bing.com");
        //创建一个wait的实例，设定超时时间为10s
        WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
        //根据name从页面上找到搜索框，并在超时时间内向搜索框键入"hello world"并模拟按下回车进行搜索。如果找不到元素不会触发ElementNotFoundException
        WebElement searchBox = wait
                .until(webDriver -> webDriver.findElement(By.name("q")));
        searchBox.sendKeys("hello world" + Keys.ENTER);

        wait.until(ExpectedConditions.elementToBeClickable(By.name("q")));

        File newScreenshot = ((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);
        FileUtils.copyFile(newScreenshot, new File("./screenshot.png"));

        driver.quit();
    }

}



[注1]:注1，如果不添加到环境变量，则需要在每个项目中指定ChromeDriver.exe的路径。
