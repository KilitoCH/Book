# 记录Html的基础知识

只包含纯Html的基础，不涉及到框架

***
## 基础语法

### 在html中使用CSS和JavaScript

这两部分应该写在head中，分别用`<link></link>`和`<style></style>`引用。使用示例：
```html
<link rel="stylesheet" href="my-css-file.css">
<script src="my-js-file.js"></script>
```

### 超链接

* 创建一个超链接只需要用`<a></a>`tag，用法示例为：
```html
<a href="https://www.mozilla.org/zh-CN/">Mozilla 主页</a>
```
即使用`href`标识想要指向的连接。在内容部分书写链接的指引文字。

* 超链接可以嵌套在其他元素中，作为其他元素的内容。用法示例：
```html
<p>这是一个指向
    <a href="https://www.mozilla.org/zh-CN/">Mozilla 主页</a>
    的超链接。
</p>
``` 

* 超链接还可以指向文件目录中的其他文件，只需要在`href`中替换网址为文件系统中对应地址。

* 超链接还可以指向当前页面的其他部分，实现页面中跳转。使用示例：
```html
<p id="paragraph_1">这是一个段落</p>
<p>这是一个指向
    <a href="#paragraph_1">其他段落</a>
    的超链接
</p>
```

* 链接到文件下载。只需要将上述`href`中的网页路径改为资源路径即可。同时可以在属性中用`download`来指定默认的保存文件名。待商榷部分。似乎并不能直接创建下载。代码示例：
```html
<a href="https://download.mozilla.org/?product=firefox-latest-ssl&os=win64&lang=zh-CN"
   download="firefox-latest-64bit-installer.exe">
  下载最新的 Firefox 中文版 - Windows（64位）
</a>
```

* 可以创建指向邮箱的链接。点击后会用默认邮件客户端打开并自动填充指定的内容。这个部分我认为不是很重要[参考链接](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks#%E7%94%B5%E5%AD%90%E9%82%AE%E4%BB%B6%E9%93%BE%E6%8E%A5)。链接中可以指定收信人、抄送、主题、主体等。示例代码：
```html
<a href="mailto:nowhere@mozilla.org?cc=name2@rapidtables.com&bcc=name3@rapidtables.com&subject=The%20subject%20of%20the%20email&body=The%20body%20of%20the%20email">
  Send mail with cc, bcc, subject and body
</a>
```

**注：** 所有的`href`中只能包含`URL`，这意味着如果包含了`URL`中所不允许的一些字符，需要进行转换。

### 文字排版

* Html文档中有默认的缩进策略，称为描述列表。使用`<dl><dt><dd>`进行描述。分别表示描述列表，描述项，具体描述。会产生自动缩进的效果。其中一个`<dt></dt>`中可以包含多个`<dd></dd>`。示例代码:
```html
<dl>
  <dt>内心独白</dt>
    <dd>戏剧中，某个角色对自己的内心活动或感受进行念白表演，这些台词只面向观众，而其他角色不会听到。</dd>
  <dt>语言独白</dt>
    <dd>戏剧中，某个角色把自己的想法直接进行念白表演，观众和其他角色都可以听到。</dd>
  <dt>旁白</dt>
    <dd>戏剧中，为渲染幽默或戏剧性效果而进行的场景之外的补充注释念白，只面向观众，内容一般都是角色的感受、想法、以及一些背景信息等。</dd>
</dl>
```

* 缩略语tag`<abbr></abbr>`，用于在缩略语下创建下划线，附加额外的标记。可用元素有`title`等。代码示例：
```html
<p>我们使用 <abbr title="超文本标记语言（Hyper text Markup Language）">HTML</abbr> 来组织网页文档。</p>
```

* 还有许多例如上下标、展示代码等等不同的标记[参考链接。](https://developer.mozilla.org/zh-CN/docs/learn/HTML/Introduction_to_HTML/Advanced_text_formatting#%E4%B8%8A%E6%A0%87%E5%92%8C%E4%B8%8B%E6%A0%87)

### 页面结构

* 常规的网络页面应该需要包含着页眉、导航栏、主内容、侧边栏、页脚等。网页
* 设计时最好保持页眉、导航栏、页脚为每个页面一致，增加复用性。然后单独设计主内容。
* 除了上述有语义的块之外，为了便于导航查询，html还提供了一些“无语义元素”。这些无语义元素可以用于定位和分隔。例如`<div></div>`和`<span></span>`。但是最好不要滥用它们，因为这会让文档的结构变得不清晰。
* html中包含了换行与水平分割线的tag。分别为`<br>`（没有闭合，放在语句后面表示换行）和`<hr>`（单独放一行，表示水平分割）。代码示例：
  ```html
  <p>示例<br>
  <hr>
  从前有个人叫小高<br>
  他说写 HTML 感觉最好<br>
  但他写的代码结构语义一团糟<br>
  他写的标签谁也懂不了。</p>
  ```

### 插入图片

* 最简单的方式就是使用`<img></img>`元素，可以包含"title","src","alt"(用于当图片无法显示时代替图片内容)等。
* 使用`<figure></figure>`。用于包含一张图片和它的标题，其中标题使用`<figcaption></figcaption>`tag表示。
* 如果要插入的图片完全是装饰用途，而与正文无关，那么可以使用css插入。这样做的坏处是css加载不出来时相当于正文少了一段。代码示例：
```css
p {
  background-image: url("figure.png");
}
```