---
title: es6
date: 2017-03-15 23:10:30
tags: es6
---

## webpack
 
```
// 这是webpack的配置文件
// 在这里可以直接写node代码
 
var path = require('path')
 
var htmlWebpackPlugin = require('html-webpack-plugin')
 
module.exports ={
    entry:path.resolve(__dirname, './src/index.js') , // 入器
    output:{
        path:'dist', // 输出目录
        filename:'bundle.js', // 输出的文件名
    },
    module:{
        loaders:[
            {
                test:/\.less$/,
                exclude:/node_modules/, // 禁止webpack去这个目录中查找
                loader:'style!css!less'  // -loader可以不写
            },
            {
                test:/\.js$/,
                exclude:/node_modules/, // 禁止webpack去这个目录中查找
                loader:'babel-loader',  // -loader可以省略
                // `npm install babel-loader --save-dev`
                query:{
                    presets:['react','es2015']
                    // `npm install babel-preset-es2015`
                    // `npm install babel-preset-react`
                }
            }
        ]
    },
    // 插件
    plugins:[
        new htmlWebpackPlugin({
            // 生成的html的文件名
            filename:'index.html',
            template:'./src/index.html' //要处理的html
        })
    ]
}
 
// loaders
// 1. less-loader 转换less语法
//  1.1 `npm install less-loader --save-dev`
//      1.1.1 `npm install less --save-dev`
//  1.2 `npm install css-loader --save-dev`
//  1.3 `npm install style-loader --save-dev`
 
// 2.babel-loader 转换其他语法为es5语法
//  2.1 `npm install babel-loader --save-dev`
//      2.1.1 `npm install babel-core --save-dev` 
//  2.2 `npm install babel-preset-es2015 --save-dev`  // 转换es6为es5
//  2.3  `npm install babel-preset-react --save-dev`  // 转换react为es5
// webpack 2.3 需要
//   `npm install webpack --save-dev`
 
 
// plugins
//  1. html-webpack-plugin  可以把html生成到输出目录,并且自动引用打包后的文件
//    `npm install html-webpack-plugin --save-dev`
 
 
```
 
 
## react
 
### 定义组件方式
 
```
// 1.引包
import React from 'react';
import TopLess from './Top.less';
 
// TodoItem
import TodoItem from '../todoitem/TodoItem.js';
import Footer from   '../footer/Footer.js'
 
// 2.创建组件
class Top extends React.Component{
    constructor(){
        super();
        // 给一些初始化的数据来显示
        this.state={
            data:[
            {id:1, name:'小胆',completed:true },
            {id:2, name:'小月',completed:true },
            {id:3, name:'小旦',completed:true },
            {id:4, name:'小一',completed:true,isShowing:false}
            ],
            newtodos:'' // 这是新添加的任务名
        }
    }
    render(){
        return(
            <section className="todoapp">
            <header className="header">
                <h1>todos</h1>
                <form  onSubmit={this.addhandler.bind(this)}>
                    <input
                    onChange={this.newtodoChange.bind(this)}
                    value={this.state.newtodos} className="new-todo" placeholder="What needs to be done?" />
                </form>
            </header>
            <section className="main">
                <input className="toggle-all" type="checkbox" />
                <label htmlFor="toggle-all">Mark all as complete</label>
                <ul className="todo-list">
                    {
                        this.state.data.map( item => {
                            return (
                                <TodoItem 
                                key={item.id}
                                myitem={item} //向子组件传值
                                mychangeTodoItem={this.changeTodoItem.bind(this)}
                                />
                                )
                        })
                    }
                </ul>
            </section>
            <Footer />
        </section>
            )
    }
    // 这个方法用来当前任务的内容
    changeTodoItem(item){
        // 遍历this.state.data
    let newData =   this.state.data.map( tmp =>{
            if(tmp.id == item.id){
                tmp.name = item.name
            }
            return tmp
        } )
    this.setState({
        data: newData
     })
    }
    // 这个方法里，只是获取文本的值，然后赋给this.state.newtodos
    newtodoChange(event){
        this.setState({
            newtodos:event.target.value
        })
    }
    //添加任务,当我按下回车键时触发
    addhandler(event){
        // 0. 禁止默认的提交事件
        event.preventDefault()
        // 如果是空字符串，就直接return,不执行后面代码
        if(!this.state.newtodos.trim()){
            return
        }
        // 1.得到用户输入的内容
        //this.state.newtodos
        // 2.把内容添加到this.state.data中。
        this.state.data.push({
            id:Math.random(),
            name:this.state.newtodos,
            completed:false
             })
        // 清空新任务
        this.state.newtodos='';
        // 为了方便操作先直接修改this.state.data的值,
        // 然后再调用 this.setState({})来更新界面
        this.setState({});
    }
}
 
// 3.暴露
// module.exports Top
// es6
export default Top
 
//子组件=======================================================================
//名字开头字母必须大写
class TodoItem extends React.Component{
    constructor(){
        super();
        this.state={
            isShowing:false
        }
    }
    render(){
        return (
            <li className={classnames({'editing':this.state.isShowing})}>
                <div className="view">
                 <input className="toggle" type="checkbox" />
                    {
                        // 双击时，显示文本框,
                        // 在文本框中编辑对应的值
                        // 在文本框中onChange事件中，调用父组件的方法,
                        // 来修改数据
                    }
                    <label
                    onDoubleClick={()=>{
                        this.setState({
                            isShowing:true
                        })
                    }}
                    >{this.props.myitem.name}</label>
                     <button className="destroy"></button>
                        </div>
                <input
                onChange={(event)=>{
                    this.props.mychangeTodoItem({
                        id:this.props.myitem.id, //子组件调用父组件传过来的东西
                        name:event.target.value
                    })
                }}
                className="edit" value={this.props.myitem.name} />
             </li>
            )
    }
    // 改变当前元素的name值
    changeTodoItem(event){
        this.props.myitem.name = event.target.value;
        this.setState({})//修改值后要手动刷新
    }
}
 
// 3.暴露出去
// module.exports
export default TodoItem
 
```
### 父组件向子组件传值
- <TodoItem   key={item.id}  myitem={item} //向子组件传值  mychangeTodoItem={this.changeTodoItem.bind(this)}   />
- 子组件使用 `{this.props.myitem.name} `
 
 
### 子组件修改父组件中的值
- 传个方法过去 
 
 
### Component生命周期
```
// 1.引包
import React from 'react';
import ReactDom from 'react-dom';
 
 
// 2.创建组件
class Life extends React.Component{
 
  // A,最先执行
  constructor(){
    super();
    this.state={
      haha:'哈哈'
    }
  }
 
  // B,这个方法会在render之前执行. 表明组件即将要添加到dom中
  componentWillMount(){
    console.log('哈哈，我是componentWillMount')
  }
 
  // C返回一个组件！
  render(){
    console.log('哈哈，我是render')
    return(
      <div id="xx">
        {this.state.haha}
      </div>
      )
  }
 
  // D.渲染完成之后的事件(表明dom结构已经生成)
  componentDidMount(){
    // 如果要做dom操作，就可以在这里进行
    console.log('哈哈！我是DidMount')
    this.setState({haha:'哈哈哈哈!'})
  }
 
  // 当调用this.setState来改变this.state时，这个方法就会被自动调用
  // 调用之后就会再调用render方法
  componentWillUpdate(){
    console.log('哈哈！ 我是WillUpdate')
  }
 
  // 这个方法会在render调用之后调用,第一次render调用时不会调用它!
  componentDidUpdate(){
    console.log('哈哈！我是DidUpdate')
  }
}
 
 
// 3.渲染组件
ReactDom.render(
  <Life />,
  document.getElementById('box')
  )
 
```