# 关于React.

1. React声明周期:

   1. Mounting: 

      componentWillMount 挂载之前的生命周期函数;

      render 渲染;

      componentDidMount 挂载完成的生命周期函数;

   2. Updating:

      componentWillReceiveProps 接收到新的props时的生命周期函数;

      shouldComponentUpdate 判断组件是否应该重新渲染, 默认是true;

      ```javascript
      shouldComponentUpdate((nextProps, nextState) => {
          return this.props.value !== nextProps.value;
      })//返回true才会重新渲染组件,返回false不会重新渲染.
      ```

      componentWillUpdate 组件将要重新渲染的生命周期函数;

      componentDidUpdate  组件重新渲染完成的生命周期函数;

   3. Unmounting:

      componentWillUnmount 组件卸载.