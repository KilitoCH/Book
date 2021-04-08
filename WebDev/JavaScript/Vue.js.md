# Vue.js

## 简要记录
* Vue.js提供了许多方式进行数据绑定，能够把Class中的数据绑定到页面元素上，这非常像当时写C#、XAML时候用的Binding，但是还是有点区别，那个直接绑定到逻辑端，也可以直接注册回调函数。但是这里绑定完了它还是在前端。
* Vue.js没有提供与后端服务器通信的接口，但是通过插件的形式实现了基于AJAX、JSONP等技术的服务端通信。

## Vue提供的属性

* `v-bind`，用于将值绑定到DOM对应的属性上。可以缩写为`:`，例如`:style`。
* `v-on`，用于动态绑定事件。可以缩写为`@`，例如`@click='doSomething`。

## 动态绑定与计算属性

* **动态绑定** Vue提供了一个很重要的特性，在DOM中书写`{{}}`相当于使用JS将这个属性绑定到一个变量上。例如：
  ```html
    <p id="example">{{data}}</p>
  ```
  代表着这个`<p>`段落的`p.text`属性被绑定到了变量`data`中。
* **计算属性** 如果`{{}}`中的js计算式过长，会导致DOM中看起来过于臃肿，这时候就可以应用计算属性。在DOM中绑定变量，然后在`Vue`实例中声明这个变量在`computed`类中，并为其赋值一个方法，用这种方法定义的变量会自动获取一个`getter`方法，当这个变量（实际上按照JS语法也是一个类）只拥有一个方法时，这就是`getter`方法，也就是我们可以直接在实例中访问这个变量。而`setter`则需要自己单独定义。计算属性最好设置为“响应式属性”，也即其依赖于另外的值进行计算，当依赖的值变化时，`computed`中的属性就会对应进行“响应式”改变。这一点即代替了监视`watch`的功能。
* **侦听器`watch`** Vue通过`watch`选项提供了更通用的监听数据变化的方法。将其实现在watch类中即可。举例：
  ```javascript
    data: {
        quesiton: '',
        answer: ''
    },
    watch: {
        question: function (newQuestion) {
            this.answer = "Waiting for typing"
        }
    }
  ```
  通过上述代码即可实现当quetion改变时设置answer为别的值。

## Class与Style绑定

### 绑定Class
可以通过给`v-bind:class`传一个对象来动态的切换class，这个对象既可以是单独的变量也可以是依赖于其他布尔值的常量也可以是类。举例：
```javascript
<div v-bind:class="{active: isActive, 'text-style': hasErrror}"></div>
<div v-bind:class="classObject"></div>

<script>
data: {
    isActive: "",
    hasError: true,
    classObject: {
        active: true,
        'text-danger': false
    }
}
</script>
```
上述语法均正确。
### 绑定内联样式
如上述所示一样。

## 条件渲染
使用`v-if`进行条件渲染，只有当值为`true`时才需要渲染。
* 如果需要控制整个分组，且不想渲染出这个元素，可以将`v-if`添加到`template`元素上，最终这个元素将不可见。
* 用`key`管理可以复用的元素。Vue会自动的复用元素而不是从头渲染，比如一系列`input`使用`v-if`控制切换时就会被复用。这会导致其中填充的内容被继承。如果不希望元素被复用则需要用key管理，为其添加唯一的`key`之后，元素会被独立。
* `v-show`，不同于`v-if`，标记为`v-show`的元素实际上我们是在控制它的`display`属性，也就是说它总是在DOM中，只是没显示。但是`v-if`为false的元素根本就不会被渲染进DOM中。

## 列表渲染
可以用`v-for`把一个数组对应为一组元素。用法为`v-for="item in items"`，语法类似于`foreach`。
* `v-for`还支持第二个可选参数，为对当前项的索引，用法为：`v-for="(item,index) in items"`，其中index就是对当前访问的item的索引。
* `v-for`还支持对对象进行遍历，遍历其中的字段。可选参数为：`v-for="(value,propertyName,index) in object"`。
* 最好在使用`v-for`的时候配套使用`key`，来为元素重新排列渲染等提供依据。
* 可以和配套属性配合使用。
* `v-for`中也可以使用值范围，即提供整数以供遍历。
* 同样的在`template`中使用`v-for`可以使得整个块被重复。

## 响应事件
参考：[事件修饰符](https://cn.vuejs.org/v2/guide/events.html#%E7%9B%91%E5%90%AC%E4%BA%8B%E4%BB%B6)。

## `v-model`
`v-model`帮助用户完成了双向绑定和事件通知。这也提供了一些修饰符，例如`.lazy`和`.number`，前者会使得更新响应变化，而后者则会自动将用户数输入转换为数值类型，如果失败则传递原始值。

## 组件基础
暂时就放一个参考的链接在这里，等待后续使用过有心得了再行完善。[参考链接](https://cn.vuejs.org/v2/guide/components-registration.html)

* 组件可以进行复用，声明其名称并全局安装之后就可以像正常html元素一样调用。
  * **组件的注册** 组件的注册分为全局注册和局部注册。全局注册需要在此组件的JS部分书写：
    ```javascript
    import ACE from './myAceEditor'

    install: function (Vue){
        Vue.component('ace',ACE)
    }
    ```
    或者在`main.js`文件中书写：
    ```javascript
    import ACE from './myAceEditor'

    Vue.component('ace',ACE)
    ```
    如果需要进行局部注册，则需要在使用此组件的地方书写：
    ```js
    import ACE from './myAceEditor'

    export default {
      components: {
        'ace': ACE,
      }
    }
    ```
  
* `router-push`依赖于页面上的`router-view`和`routers`表。页面的路由层次取决于路由表中书写的层次。
* `slot`类似于“留白”。即在组件中留出一定的余地，当有需要时再在引用这个组件的时候“填充进去”。
* `$emit`&`prop`分别为子组件向父组件传值和传递方法的方法。

## Vue JS Crash Course 2021/Youtube

### Notes
* `Fetch API`
* `async await` 

* `json-server`