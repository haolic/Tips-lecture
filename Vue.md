# 关于Vue2.



1. Vue2中响应式的属性必须用v-bind:来绑定到元素上,不能直接写上去.

   1. ```javascript
      <div v-bind:data-props="value"></div>//value是响应的,默认值是初始化的值.
      <div data-props="value"></div>//value不是响应的,默认值就是字符串"value".
      ```

   2. ​