# wiki
总结
React-router页面传递参数的几种方法
使用的router为react-router-dom
1．props.match 
<Route path="/user/:username" component={User}/>
获取数据this.props.match.params.username
这种方法可以得到一个或多个值，但是每个值的类型都是字符串，不能传递对象，如果传递的话可以将对象转换成json字符串来传递。
2.search
Route配置
<Route path=’/about’ component={About}/>
使用let path = {
pathname:'/about',
search:'?name=tom',
hash:'#the-hash'
}
使用this.props.history.push(path)
<Link to={path}/>
获取数据this.props.location.search得到?name=tom
search以及hash的值会拼接在url上/about?name=tom#the-hash
如果search里有中文，在url里不会是中文，但是在this.props.location.search得到的值会被转义
3.state
使用
<Link to={{
  pathname: '/user',
  state: { name: ‘tom’}
}}/>

this.props.history.push({pathname:'/ user'', state:{ name: ‘tom’}})
获取数据
This.props.location.state
这种方法传递的参数不会再URL上显示
其实这个state可以换成任意别的值
2.withRouter
正常情况下只有Router的component组件能够自动带有三个属性history，location，match，
如果组件需要用到这几个属性怎么办呢，可以用withRouter，
withRouter是一个高阶组件，可以包装任何自定义组件，将react-router的history，location，match三个对象传入
用法
import {withRouter} from ‘react-router-dom’;
@withRouter
class App extends React.Component{
	constructor(props){
		super(props)
	}
	handleClick = ()=>{
		this.props.history.push(‘/about’)
}
	render(){
	<button onClick={handleClick}>jump</button>
}
}
