### 修改vue里面定义好的数据

	var app= new Vue({
	el:"#app",
		data:{
			message:"hello world"
		}
	})
	app.$data.message= 'bye world'

### todolist在输入框输入“数据”，添加到list里面

    //html
	<div id="app">
	    <input type="text" v-model="inputValue">
	    <button @click="add">提交</button>
	    <ul>
	        <li v-for="item in list">{{item}}</li>
	    </ul>
	</div>
    //js
	var app=new Vue({
	         el:'#app',
	         data:{
	             list:[
	                 "第一节课",
	                 "第二节课",
	                 "第三节课"
	             ],
	          inputValue : ''
	        },
	        methods:{
	            add:function (){
	                this.list.push(this.inputValue);
	            }
	        }
	
	
	    })

### mvp模式和mvvm模式
 #### view视图presenter控制器model模型（存储数据的地方）
 mvp模式核心是presenter控制器层，presenter操作dom修改view，很少用到ajax请求
![](https://i.imgur.com/PyoBUpQ.jpg)
#### mvvm model view vue(vm)
![](https://i.imgur.com/1Mj5wod.jpg)

使用vue开发可以减少代码量，至少减少30%

### 前端组件化
一个页面有很多部分组成，把页面上的模块进行拆分，一个模块一个页面方便维护

### 全局组件与局部组件的使用（以及父组件对子组件的传值，通过v-bind实现）

全局组件
list定义在本地data里面，通过v-bind:content="item"重新命名，把item传入模板内部，但是需要props接收。然后才能在template里面使用变量content


	//html
	<todo-list v-bind:content="item" v-for="item in list"></todo-list>
	//js
    Vue.component("todoList",{
        props:["content"],
        template:"<li>{{content}}</li>"
    })

局部组件

    //html
	<todo-list v-bind:content="item" v-for="item in list"></todo-list>
	//本地声明
	var todoList={
	    props:["content"],
	    template:"<li>{{content}}</li>"
	}
    //vue里面的components调用
	components:{
	             todoList（新起的名字）:todoList（原名字）
	        }

### 子组件对父组件的传值
（子组件$emit传递事件，父组件监听事件，达到数据传递目的）

在子组件里面新增methods方法，绑定一个delete事件。使用$emit方法实现，前面是事件名字，后面是传递的参数

    methods:{
        handleBtnClick:function (){
            this.$emit("delete",this.index);
        }
    }

父组件用handleBtndelete方法绑定接收delete事件，进行下一步处理

 	<todo-list  v-bind:content="item" v-bind:index="index" 
	v-for="(item,index) in list" @delete="handleBtndelete"></todo-list>


### Vue实例
new Vue是根实例，每个组件也都是实例。实例上面有很多方法比如$destroy,$emit等
### Vue的生命周期
生命周期函数就是vue实例在某一个时间点会自动执行的函数
beforeCreate,
created,
beforeMount,//挂载之前（未被渲染）
mounted,//挂载之后（已经被渲染）
beforeDestroy,
destroyed,
beforeUpdate,
updated
![](https://i.imgur.com/TeGabtm.png)