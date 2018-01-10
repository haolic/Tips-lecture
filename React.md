# 关于React.

1. React生命周期:

   1. Mounting: 挂载阶段.

      getDefaultProps 初始化属性;

      getInitialState 初始化状态;

      componentWillMount 挂载之前的生命周期函数;

      render 渲染;

      componentDidMount 挂载完成的生命周期函数;

   2. Updating: 执行中阶段(更新阶段).

      componentWillReceiveProps 接收到新的props时的生命周期函数;

      shouldComponentUpdate 判断组件是否应该重新渲染, 默认是true;

      ```javascript
      shouldComponentUpdate((nextProps, nextState) => {
          return this.props.value !== nextProps.value;
      })//返回true才会重新渲染组件,返回false不会重新渲染.
      ```

      componentWillUpdate 组件将要重新渲染的生命周期函数;

      render 组件重新渲染;

      componentDidUpdate  组件重新渲染完成的生命周期函数;

   3. Unmounting: 卸载阶段.

      componentWillUnmount 组件卸载.

2. 路由传值:

   1. /page1/:name/:age/:sex

      子路由用下面方式接数据.

      this.props.params.name

   2. /page1?name=wangsan&pwd=123

      子路由用下面方式接数据.

      this.props.location.query.name

3. 子组件给父组件传值:

   1. 通过触发子组件方法例如onChange来调用绑定到子组件上的一个函数fn, 并且此函数将子组件的某个值val当实参传递, 同时, 在子组件props.fn上绑定父组件的一个函数来调用setState方法,从而将值传递给父组件.

      1. ```jsx
         //子组件，handleVal函数处理用户输入的字符，再传给父组件的handelEmail函数
         var Child = React.createClass({
             handleVal: function() {
                 var val = this.refs.emailDom.value;
                 val = val.replace(/[^0-9|a-z|\@|\.]/ig,"");
                 this.props.handleEmail(val);
             },
             render: function(){
                 return (
                     <div>
                         请输入邮箱：<input ref="emailDom" onChange={this.handleVal}/>
                     </div>
                 )
             }
         });
         //父组件，通过handleEmail接受到的参数，即子组件的值
         var Parent = React.createClass({
             getInitialState: function(){
                 return {
                     email: ''
                 }
             },
             handleEmail: function(val){
                 this.setState({email: val});
             },
             render: function(){
                 return (
                     <div>
                         <div>用户邮箱：{this.state.email}</div>
                         <Child name="email" handleEmail={this.handleEmail.bind(this)}/>
                     </div>
                 )
             }
         });
         React.render(
           <Parent />,
           document.getElementById('test')
         );
         ```

      2. ​

