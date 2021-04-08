# JS基础

## 定位元素与代码风格
在js中可以使用函数来定位dom中的元素，且根据存储的变量访问元素本身和他的父亲、兄弟节点。良好的代码风格是将所有样式格式放在css文件中，将所有的js部分放在函数中，方便进行修改和调试，也就是说区分出显示和动态功能的区别。

## 数组
js中的数组类似于其他语言中的集合，特别是python里的。

## 一些有用的方法
* `pop() & push()`方法，分别是在数组末尾删除和添加元素。
* `unshift() & shift()`方法，分别是在数组头删除和添加元素。

## JavaScript模块

## 在js中处理文件

相关接口：`File`和`Blob`。其中`File`继承自`Blob`。可以使用他们相关的方法来操作、读取文件。
利用这两个类和一些H5特性，我们可以实现在网页中读取、拖拽选择文件等。

参考：[在web应用程序中使用文件](https://developer.mozilla.org/zh-CN/docs/Web/API/File/Using_files_from_web_applications)。
[Blob](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)
[File](https://developer.mozilla.org/zh-CN/docs/Web/API/File)