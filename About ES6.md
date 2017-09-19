# 分享一下[我所了解的ES6/2015](https://github.com/haolic/ECMAScript6)^_^

---

1. str.repeat(num)方法: 重复str字符串num次. 存在弱类型转换, 如果参数num不是数值, 会先转换成number. 但是这里的弱类型转换跟parseInt()有所不同:
   1. parseInt()会将以数字开头的字符串(如"123abc")转换成123,但是repeat()参数不是数值则str.repeat()会返回空字符串( "" );
   2. 'abc'.repeat(-1)// 报错;
   3. 'abc'.repeat(0)// '';
   4. 'abc'.repeat(3.5)// 'abcabcabc', 会把小数先转换为整数;
   5. 'abc'.repeat(NaN)// '';

2. ​babel中的语法极其类似ES6, 很神奇,或者说不是类似, 而是确实是ES6.

3. ```javascript
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

   ​

   ​