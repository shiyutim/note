# React

## 导航

- [创建项目](#创建项目)
- [基本使用](#基本使用)

### 创建项目
1. 安装脚手架 `npm i create-react-app`
2. 创建项目 `create-react-app xxx`

### 基本使用
1. `ReactDom.render()` 方法用于将模板插入指定的 DOM 节点。

    ```
    ReactDom.render(
        <h1>Hello world!</h1>,
        document.querySelector('#app')
    )
    ```
    
    将一个 `h1` 标题插入 `#app`的 DOM 节点里面。
    
2. `class`类需要写成`className`，`for` 需要写成 `htmlFor`。因为 `class` 和 `for` 在 JavaScript 中是保留字。
3. 组件声明有两种方式，分别为*函数组件*和*class组件*。
    - 函数组件
    
    ```
    function Hello(props) {
        render() {
            <div>hello {this.props.name}</div>
        }
    } 
    ```
    
    - class 组件
    
    ```
    class Hello extends React.Component{
        constructor(props) {
            super(props)
            this.state = {
                name: 'tim'
            }
        }
        
        render() {
            return (
                <div> hello {this.state.name} </div>
            )
        }
    }
    ```
    
    需要注意的是，组件名称必须以大写字母开头，因为 React 会将以小写字母开头的组件视为原生 DOM 标签。
    
4. `this.state = {}`里面用于添加本组件的值。 `this.setState({})` 用于更改值。
5. 如果要获取表单的值，可以设置一个 `onChange`的函数，然后通过 `event.target.value` 来获取*表单的值*。
6. 组件的生命周期分成三个状态：

    ```
     Mounting：已插入真实 DOM
     Updating：正在被重新渲染
     Unmounting：已移出真实 DOM
    ```
    
    React 为每个状态都提供了两种处理函数，`will` 函数在进入状态之前调用，`did` 函数在进入状态之后调用，三种状态共计五种处理函数。
    
    ```
     componentWillMount()
     componentDidMount()
     componentWillUpdate(object nextProps, object nextState)
     componentDidUpdate(object prevProps, object prevState)
     componentWillUnmount()
    ```
    
    React 还提供两种特殊状态的处理函数。
    
    ```
    componentWillReceiveProps(object nextProps)：已加载组件收到新的参数时调用
    shouldComponentUpdate(object nextProps, object nextState)：组件判断是否重新渲染时调用
    ```