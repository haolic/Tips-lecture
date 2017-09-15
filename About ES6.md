# 分享一下[我所了解的ES6/2015](https://github.com/haolic/ECMAScript6)^_^

---

1. str.repeat(num)方法: 重复str字符串num次. 存在弱类型转换, 如果参数num不是数值, 会先转换成number. 但是这里的弱类型转换跟parseInt()有所不同:
   1. parseInt()会将以数字开头的字符串(如"123abc")转换成123,但是repeat()参数不是数值, str.repeat()会返回空字符串( "" );
2. ​