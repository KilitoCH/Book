# Selenium
## Behavior-driven development (BDD)
BDD is also an iterative development methodology based on the above TDD, in which the goal is to involve all the parties in the development of an application.

Each cycle starts by creating some specifications (which should fail). Then create the failing unit tests (which should also fail) and then do the development.

This cycle is repeated until all types of tests are passing.

In order to do so, a specification language is used. It should be understandable by all parties and simple, standard and explicit. Most tools use ***Gherkin*** as this language.

The goal is to be able to detect even more errors than TDD, by targeting potential acceptance errors too and make communication between parties smoother.

A set of tools are currently available to write the specifications and match them with code functions, such as ***Cucumber*** or ***SpecFlow***.

A set of tools are built on top of Selenium to make this process even faster by directly transforming the BDD specifications into executable code. Some of these are ***JBehave***, ***Capybara*** and ***Robot Framework***.

## Docs
***
If there is an issue with the documentation, we want to know! The best way to communicate an issue is to visit https://github.com/seleniumhq/seleniumhq.github.io/issues and search to see whether or not the issue has been filed already. If not, feel free to open one!

Many members of the community frequent the #selenium IRC channel at irc.freenode.net. Feel free to drop in and ask questions and if you get help which you think could be of use within these documents, be sure to add your contribution! We can update these documents, but it is much easier for everyone when we get contributions from outside the normal committers.
## Install for Java
***
Java
Installation of Selenium libraries for Java can be done using Maven. Add the selenium-java dependency in your project pom.xml:
``` java
<dependency>
  <groupId>org.seleniumhq.selenium</groupId>
  <artifactId>selenium-java</artifactId>
  <version>3.X</version>
</dependency>
```
The selenium-java dependency supports running your automation project with all Selenium supported browsers. If you want to run tests only in a specific browser, you can add the dependency for that browser in your pom.xml file. For example, you should add following dependency in your pom.xml file to run your tests only in Firefox:
``` java
<dependency>
  <groupId>org.seleniumhq.selenium</groupId>
  <artifactId>selenium-firefox-driver</artifactId>
  <version>3.X</version>
</dependency>
```
In a similar manner, if you want to run tests only in Chrome, you should add the following dependency:
``` java
<dependency>
  <groupId>org.seleniumhq.selenium</groupId>
  <artifactId>selenium-chrome-driver</artifactId>
  <version>3.X</version>
</dependency>
```
### **Installing Standalone server**
If you plan to use Grid then you should download the selenium-server-standalone JAR file. All the components are available via selenium-server. The standalone JAR contains everything, including the remote Selenium server and the client-side bindings. This means that if you use the selenium-server-standalone jar in your project, you do not have to add selenium-java or a browser specific jar.
``` java
<dependency>
 <groupId>org.seleniumhq.selenium</groupId>
 <artifactId>selenium-server</artifactId>
 <version>3.X</version>
</dependency>
```
## WebDriver
