# **一些学习中的Tips.**

---

1. 变量提升.概念: 后var的变量如果在var之前操作,不会报错,会以undefined来操作,称为变量提升.let声明的变量不会被提升.

2. 同源策略.由Netscape提出的安全策略,同源是指协议,域名,端口相同,执行脚本时会检查脚本属于哪个页面,只有同源的脚本才会被执行.

3. JSON.stringify(obj)把对象转换成json.

4. web标准:Web标准，不是一个标准,是一些列标准。Web标准由万维网联盟（W3C）制定。包括网站三层:结构层,表现层,动作层的标准,结构层标准主要是规定html,xhtml,xml的相关规范,表现层标准主要包括css的规范,动作层标准包含w3c dom模型,ECMAScript等规范.

5. 几个兼容性问题:

  ​

  阻止冒泡:

  ```javascript
  e.stopPropagation();//IE9+
  e.cancelBubble = true;//ie6/7/8;
  ```
  事件对象:

  ```javascript
  window.event;//ie6/7/8;
  function(e){}//其中的e.ie9+;
  ```
  阻止默认事件:

  ```javascript
  e.preventDefault();//ie9+;
  returnValue = false;//IE6/7/8
  ```
  获取滚动条位置:

  ```javascript
  window.pageYOffset;//IE9+
  document.documentElement.scrollTop;//IE6/7/8
  ```

  同时阻止冒泡和默认事件:

  ```javascript
  return false;//在事件处理函数末尾写return false.
  ```

6. js执行流程流程中第一阶段会创建所有变量,并赋值为undefined,(hoisting(变量声明提升)机制)对象如果添加属性并赋值,也会遵循变量声明提升.

7. typeof 正则表达式;----返回object;

8. if语句里声明函数,在strict mode出现之前,在if内声明函数是没有一致性的,不同浏览器会做出不同解释,最佳的代码规范都要求不在if里声明函数.

9. ECMAScript中的对象分类：

   1. 本地对象：js中的构造器函数（类）;
   2. 宿主对象：所有非本地对象都是宿主对象，即由 ECMAScript 实现的宿主环境提供的对象。
   3. 内置对象：ECMA-262只定义了两个内置对象，即 Global 和 Math （它们也是本地对象，根据定义，每个内置对象都是本地对象）。

10. 暂时性死区:

  块级作用域内存在let命令, 就会绑定这块儿区域, let声明的变量如果在声明之前操作,会报错, 即:

  ```javascript
  var temp = 123;
  if (true) {
    temp = 456;//报错
    let temp;
  }
  ```

  例如上述代码中let绑定了这个区域,所以会报错.

  总之, 在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称TDZ）。

11. nodejs: 服务器端js的运行环境.

12. jsonp: json with padding, 用json填充函数的实参. 其本质上是利用<script> 标签的src属性可以跨域的原理来实现跨域.

13. 原型链: 一条由__proto__串起来,直到 Object().prototype.__proto__为null的链, 称为原型链.

14. 由于Function的特殊性，它“自己构造自己”。

    ```javascript
    Function.__proto__ === Function.prototype //true
    ```

15. 冻结的对象: 

    ```javascript
    const foo = Object.freeze({});
    //常规模式给foo对象添加属性不起作用;
    //严格模式给foo添加属性报错;
    foo.prop = 111;//报错
    ```

    常量foo指向一个冻结的对象，所以添加新属性不起作用，严格模式时还会报错。

    出了将对象本身冻结, 对象的属性也应该被冻结:

    ```javascript
    var oFree = (obj) {
      Object.freeze(obj);
      Object.keys(obj).forEach( (key, value) => {
        if( typeof obj[key] === 'object' ) {
          oFree(obj[key]);
        }
      });
    };
    ```

16. let 声明的变量不属于全局变量:

    ```javascript
    var a = 1;
    window.a // 1
    //===============
    let a = 1;
    window.a //undefined
    ```

17. 解构赋值中, 实际上只要等号左右两边结构相同就会赋值成功. 不成功的变量就会是undefined:

    ```javascript
    let [foo, [[bar], baz]] = [1, [[2], 3]];
    foo // 1
    bar // 2
    baz // 3
    //==============================================
    let [x, y, ...z] = ['a'];
    x // "a"
    y // undefined
    z // []
    ```

18. 为什么扩展js内置对象不是一个好的做法：

    由于扩展内置对象会有种种不确定性, 不保证JavaScript后续会原生支持扩展的方法, 一旦支持, 就会跟自己扩展的起冲突.导致代码崩溃.

19. jQuery自定义插件的方法: 

    ```javascript

    1.
    jQuery.fn.extend({
        "exFn": function(){alert('jquery对象扩展插件')}
    });
    2.
    jQuery.extend({
        "exFn": function(){alert('jquery核心对象方法')}
    });
    ```

20. ES6的对象的解构赋值与数组解构赋值的区别: 

    数组解构赋值是根据元素位置赋值, 由于对象是无序的属性值对, 所以解构赋值时需要注意, 同名的属性才会被赋值成功(根据对象的属性名来赋对应的值).

21. a标记的target属性: 

    1. _blank :在新窗口打开链接
    2. _self: 在当前窗开打开链接
    3. _top: 在最顶级的窗口打开链接
    4. _parent: 在父窗口打开链接

22. [数组排序:](https://github.com/haolic/Tips-lecture/tree/master/example/%E6%95%B0%E7%BB%84%E6%8E%92%E5%BA%8F) 

    1. [sort()方法](https://github.com/haolic/Tips-lecture/blob/master/example/%E6%95%B0%E7%BB%84%E6%8E%92%E5%BA%8F/sort()%E6%8E%92%E5%BA%8F.html)
    2. [二分法](https://github.com/haolic/Tips-lecture/blob/master/example/%E6%95%B0%E7%BB%84%E6%8E%92%E5%BA%8F/%E4%BA%8C%E5%88%86%E6%B3%95%E6%8E%92%E5%BA%8F.html)
    3. [选择排序](https://github.com/haolic/Tips-lecture/blob/master/example/%E6%95%B0%E7%BB%84%E6%8E%92%E5%BA%8F/%E9%80%89%E6%8B%A9%E6%8E%92%E5%BA%8F.html)
    4. [冒泡排序](https://github.com/haolic/Tips-lecture/blob/master/example/%E6%95%B0%E7%BB%84%E6%8E%92%E5%BA%8F/%E5%86%92%E6%B3%A1%E6%8E%92%E5%BA%8F.html)

23. [数组去重: 6种方法.](https://github.com/haolic/Tips-lecture/tree/master/example/%E6%95%B0%E7%BB%84%E5%8E%BB%E9%87%8D)

24. angular中ng-repeat指令:

    ```javascript
    <ul>
      <li ng-repeat="(index, value) in array">
      	//index为下标.
        //value为数组元素.
      </li>
    </ul>
    ```

    ​

25. ng-model指令详解:

    1. ```javascript
       //对于input:text, ng-model绑定的值为元素的value.
       <input type="text" ng-model="value">
       //此处的"value"是domElement.value.
       ```

    2. ```javascript
       //对于input:password, ng-model绑定的值为元素的value.
       <input type="password" ng-model="value">
       //此处的"value"是domElement.value.
       ```

    3. ```javascript
       //对于textarea, ng-model绑定的值为元素的value.
       <textarea ng-model="value"></textarea>
       //此处的"value"是domElement.value.
       ```

    4. ```javascript
       //*此条完整性有待完善.
       //对于input:checkbox/radio, ng-model绑定的值为元素的checked的值(true/false).
       <input type="checkbox" ng-model="checked">
       <input type="radio" ng-model="checked">
       //此处的"checked"是domElement.checked.
       ```

26. Vue2中v-model的.lazy修饰符, 是使得input的输入内容在失去焦点时响应数据变化.

27. DOM节点操作:

    1. 创建节点:

       ```javascript
       document.createElement(nodeName);
       ```

    2. 在某个节点前插入节点:

       ```javascript
       document.insertBefore(newNode, oldNode);
       ```

    3. 复制(clone)节点:

       ```javascript
       cloneNode(true | false);
       ```

    4. 删除节点: 

       ```javascript
       parentNode.removeChild(node);
       ```

       ​

28. ajax中阻止缓存: 

    1. jquery中cache: false
    2. 在URL参数后加上 "?timestamp=" + new Date().getTime();

29. src和href的区别: src是加载静态资源比如加载图片、加载js, href是超链接的写法,一般用来给某标记或文字设置超链接. 浏览器解析到src时,会暂停其他资源下载,直到将该资源加载-编译-执行完毕.浏览器解析到href会不停止对当前文档的处理,并行下载资源.

30. 事件委派(委托)的实现原理: 通过给父元素添加事件, 通过事件冒泡并且通过event.target来获取实际想要触发事件的对象来实现委派.

31. GET和POST区别：

    1. GET是和请求头一起发送数据, 大小有限制, 但是速度快；
    2. POST是和请求体（正文）一起发送，大小没有限制。

32. 判断object的具体类型: Object.prototype.toString.call(obj)判断obj的具体类型;

    ​	由于typeof(array)/ typeof(null)/ typeof(obj)均返回object所以需要用上述方法判断具体类型.

33. 有关web性能:

    1. web性能时间: 从用户输入网址回车到整个网站(或部分)显示到用户面前所花的时间.
       1. dns解析时间: 
          1. 减少DNS解析时间:国内尽量用中国万网域名.
       2. 网页下载时间: 
          1. 减少冗余代码(纯手写), 
          2. 减少http请求(css/js 合并&压缩, css sprites/webpack打包).
       3. 浏览器渲染时间: 
          1. css 高效能: 书写顺序(位置属性, 大小, 文本, 背景, 其他(animation, transition)))

34. 类数组转换成数组: 

    1. Array.prototype.slice.call(arrayLike);//slice([a,[b]])方法返回值为数组.无参数返回整个数组,一个参数slice(a)返回从下标为a到最后的数组,两个参数slice(a,b) 返回从下标a到b且不包含下标为b的元素.
    2. Array.prototype.splice.call(arrayLike);//splice();方法返回值也为数组,但是会对原数组有影响. 例如splice(0)是从第0个下标的元素删除到最后一个元素,随后原数组中元素个数为空.splice(a,b)为从下标为a删除到下标为b,且不包含b.

35. 两个日期对象相减,获得的是时间戳的差.

    1. ```javascript
       var date1 = new Date();
       var date2 = new Date(2017, 1, 1, 12, 59, 59);
       var str = date1 = data2;//str为时间戳的差.
       ```

---

以后会不定期更新.哈哈哈 .