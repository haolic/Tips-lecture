# 分享一下[我所了解的ES6/2015](https://github.com/haolic/ECMAScript6)^_^

---

1. str.repeat(num)方法: 重复str字符串num次. 存在弱类型转换, 如果参数num不是数值, 会先转换成number. 但是这里的弱类型转换跟parseInt()有所不同:
   1. parseInt()会将以数字开头的字符串(如"123abc")转换成123,但是repeat()参数不是数值则str.repeat()会返回空字符串( "" );
   2. 'abc'.repeat(-1)// 报错;
   3. 'abc'.repeat(0)// '';
   4. 'abc'.repeat(3.5)// 'abcabcabc', 会把小数先转换为整数;
   5. 'abc'.repeat(NaN)// '';

2. babel中的语法极其类似ES6, 很神奇,或者说不是类似, 而是确实是ES6.

3. 反单引号函数调用:

   1. ```javascript
      反单引号调用函数
      (foo`haha${a + b}heihei${c + d}`)的情况: 
      会把模板字符串分解开, 
      例如foo`haha${a + b}heihei${c + d}`
      会将``中间的部分分解成:
      ['haha', 'heihei', ''],
      ${a + b}的值, 
      ${c + d}的值,三部分.
      其中第一个参数是数组并且最后一个元素是空字符串'';
      ```

4. Promise对象:

   1. new Promise()需要传入一个函数, 注意:一旦new Promise()不但会创建一个Promise对象, 并且执行了传入的函数.

      ```javascript
      let p = new Promise(function (resolve, reject) { console.log('something') })//此处不仅创建了Promise对象, 并且执行了传入的函数.
      ```

   2. Promise.all():并行执行传入的每个函数

      ```javascript
      Promise.all([fun1(), fun2(), fun3()]).then(function(value){})//等待慢的, 当fun1/2/3都执行完之后才调用then的回调.并且value为一个数组,数组的元素是每个func中resolve传入的值.
      ```

   3. Promise.race():并行执行传入的每个函数

      ```javascript
      Promise.race([fun1(), fun2(), fun3()]).then(function(value){})//优先照顾快的, 当fun1/2/3任一个执行完成就调用then中的回调, value为最先执行完的函数的resolve传入的值.
      ```

      但执行then中的回调的同时并不会停止执行剩余未执行函数.

5. Set()结构中, undefined/null/NaN/Infinity不会重复出现.