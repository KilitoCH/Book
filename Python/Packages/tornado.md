# tornado
Tornado 是一个Python的包. 它在PyPI的主页是[tornado·PyPI](https://pypi.org/project/tornado/).tornado是一个Python的Web框架，还是一个异步网络库。参考文档地址：[tornado Introduction](https://www.tornadoweb.org/en/stable/guide/intro.html).

## 简介
Tornado 能够被简单地分成四个部分:
* 一个Web框架。
* HTTP的服务器端和异步客户端的实现。
* 包含了例如类`IOLoop`和`IOStream`的异步网络库。这些库是HTTP组件的基础部分，同时也可以用来实现其他协议。
* 能够使得异步代码更易于开发的协同程序库。
  
> 如果希望使用Tornado的所有优势，可以将tornado的Web框架和HTTPServer结合使用。

## 异步和非阻塞I/O
一般来说Web工作在同步状态，为每个连接开支一个线程。但是异步工作状态下，一个线程就可以完成所有工作，通过轮询的方式对每个人服务。

### 阻塞
在开发过程中我们会遇到许多阻塞的场景，甚至有时候需要考虑到CPU的阻塞，应该尽量避免。

### 异步
* 首先区分异步函数和同步函数，同步函数必须执行完所有语句之后才会返回，但是异步函数会直接返回（说实话这里都不能叫返回值了，我觉得取个别的名字更好，后续完善）。
一个异步接口可能有以下的特性：
* 回调（Callback）参数
* 返回一个`placeholder`（例如`Future`,`Promise`,`Deferred`）
* 能被放在一个队列中
* 注册回调(Callback)
* 除了一些底层组件，例如`IOLoop`，Tornado中的操作通常会返回`placeholder`对象`Futures`。`Futures`通常包含`await`,`yield`关键字，并且被传递到结果中。
