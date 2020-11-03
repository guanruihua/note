---
title: vue-expand
date: 2020-09-22 21:49:35
tags:
	- vue
	- expand
	- javascript
	- front-end
---



# vue-expand

## 常用webpack配置

### **vue-lic3脚手架（vue.config.js）**

#### publicPath

类型：String

默认：'/'

部署应用包时的基本 URL。默认情况下，Vue CLI会假设你的应用是被部署在一个域名的根路径上，例如https://www.my-app.com/。如果应用被部署在一个子路径上，你就需要用这个选项指定这个子路径。例如，如果你的应用被部署在https://www.my-app.com/my-app/，则设置publicPath为/my-app/

这个值也可以被设置为空字符串 ('') 或是相对路径 ('./')，这样所有的资源都会被链接为相对路径，这样打出来的包可以被部署在任意路径，也可以用在类似 Cordova hybrid 应用的文件系统中。

#### productionSourceMap

类型：boolean

moren：true

不允许打包时生成项目来源映射文件，在生产环境下可以显著的减少包的体积

> 注 Source map的作用：针对打包后的代码进行的处理，就是一个信息文件，里面储存着位置信息。也就是说，转换后的代码的每一个位置，所对应的转换前的位置。有了它，出错的时候，除错工具将直接显示原始代码，而不是转换后的代码。这无疑给开发者带来了很大方便

#### assetsDir

放置生成的静态资源 (js、css、img、fonts) 的 (相对于 outputDir 的) 目录,默认是'',

#### indexPath

指定生成的 index.html 的输出路径(相对于outputDir)。也可以是一个绝对路径。默认是'index.html'

#### lintOnSave

是否在每次保存时使用eslint检查，这个对语法的要求比较严格，对自己有要求的同学可以使用

#### css

```js
css: {
    //是否启用css分离插件，默认是true，如果不启用css样式分离插件，打包出来的css是通过内联样式的方式注入至dom中的，
    extract: true,
    sourceMap: false,//效果同上
    modules: false,// 为所有的 CSS 及其预处理文件开启 CSS Modules。
    // 这个选项不会影响 `*.vue` 文件。
  },
```

#### devServer

本地开发服务器配置

```js
devServer: { 
    //配置开发服务器
    host: "0.0.0.0",
    //是否启用热加载，就是每次更新代码，是否需要重新刷新浏览器才能看到新代码效果
    hot: true,
    //服务启动端口
    port: "8080",
    //是否自动打开浏览器默认为false
    open: false,
    //配置http代理
    proxy: { 
      "/api": { //如果ajax请求的地址是http://192.168.0.118:9999/api1那么你就可以在jajx中使用/api/api1路径,其请求路径会解析
        // http://192.168.0.118:9999/api1，当然你在浏览器上开到的还是http://localhost:8080/api/api1;
        target: "http://192.168.0.118:9999",
        //是否允许跨域，这里是在开发环境会起作用，但在生产环境下，还是由后台去处理，所以不必太在意
        changeOrigin: true,
        pathRewrite: {
            //把多余的路径置为''
          "api": ""
        }
      },
      "/api2": {//可以配置多个代理，匹配上那个就使用哪种解析方式
        target: "http://api2",
        // ...
      }
    }
},
```

#### pluginOptions

这是一个不进行任何 schema 验证的对象，因此它可以用来传递任何第三方插件选项，例如：

```js
{
    //定义一个全局的less文件，把公共样式变量放入其中，这样每次使用的时候就不用重新引用了
    'style-resources-loader': {
      preProcessor: 'less',
      patterns: [
        './src/assets/public.less'
      ]
    }
}
```

#### chainWebpack

是一个函数，会接收一个基于 webpack-chain 的 ChainableConfig 实例。允许对内部的 webpack 配置进行更细粒度的修改。例如：

```js
chainWebpack(config) { 
//添加一个路径别名 假设有在assets/img/menu/目录下有十张图片，如果全路径require("/assets/img/menu/img1.png")
//去引入在不同的层级下实在是太不方便了，这时候向下方一样定义一个路劲别名就很实用了
    config.resolve.alias
      //添加多个别名支持链式调用
      .set("assets", path.join(__dirname, "/src/assets"))
      .set("img", path.join(__dirname, "/src/assets/img/menu"))
      //引入图片时只需require("img/img1.png");即可
}
```

## 组件传值

#### 父传子

通过props传递

```
父组件： <child value = '传递的数据' />

子组件: props['value'],接收数据,接受之后使用和data中定义数据使用方式一样
```

#### 子传父

在父组件中给子组件绑定一个自定义的事件，子组件通过$emit()触发该事件并传值。

```
父组件： <child @receive = 'receive' />

 子组件: this.$emit('receive','传递的数据')
```

#### 兄弟组件传值

- 通过中央通信 let bus = new Vue()

> A：methods :{ 函数{bus.$emit(‘自定义事件名’，数据)} 发送

> B：created （）{bus.$on(‘A发送过来的自定义事件名’，函数)} 进行数据接收

- 通过vuex



## **v-for key的作用**

当Vue用 v-for 正在更新已渲染过的元素列表是，它默认用“就地复用”策略。如果数据项的顺序被改变，Vue将不是移动DOM元素来匹配数据项的改变，而是简单复用此处每个元素，并且确保它在特定索引下显示已被渲染过的每个元素。

为了给Vue一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 key 属性。key属性的类型只能为 string或者number类型。

key 的特殊属性主要用在Vue的虚拟DOM算法，在新旧nodes对比时辨识VNodes。如果不使用 key，Vue会使用一种最大限度减少动态元素并且尽可能的尝试修复/再利用相同类型元素的算法。使用key，它会基于key的变化重新排列元素顺序，并且会移除 key 不存在的元素。

## **Vue的双向数据绑定原理**

vue.js 是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。主要分为以下几个步骤：

> 1、需要observe的数据对象进行递归遍历，包括子属性对象的属性，都加上setter和getter这样的话，给这个对象的某个值赋值，就会触发setter，那么就能监听到了数据变化

> 2、compile解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图

> 3、Watcher订阅者是Observer和Compile之间通信的桥梁，主要做的事情是: ①在自身实例化时往属性订阅器(dep)里面添加自己 ②自身必须有一个update()方法 ③待属性变动dep.notice()通知时，能调用自身的update()方法，并触发Compile中绑定的回调，则功成身退。

> 4、MVVM作为数据绑定的入口，整合Observer、Compile和Watcher三者，通过Observer来监听自己的model数据变化，通过Compile来解析编译模板指令，最终利用Watcher搭起Observer和Compile之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据model变更的双向绑定效果。





## vue-loader

> vue文件加载器, 跟template/js/style转换为js模块

## vuex

> 状态管理模式来纪中管理状态或信息

### 使用vuex

store.js

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Strore({
  state: {
    count : 1,
    msg: 'msg',
  },
  mutations: {
    
  }, 
  action: {
    
  }
})
```

app.js

```js
export default {
  data(){
    return ({
      msg: 'hello',
    })
  },
  computed: {
    count() {
      return this.$store.state.count;//获取单个状态
    }
  }
}
```

### State

store.js

```js
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex);

export default new Vuex.Store({
  state: {
    count: 0,
    msg: 'msg'
  }
})
```

app.vue

```js
import { mapState } from 'vuex'
export defualt {
  data(){
    msg: 'grh',
  }
  //方法一
  computed: mapState({
    msg() {
     return this.msg + 'hello'; 
    },
    msg2(state) {
      return state.msg;
    }
  })
   //方法二: 使用解构符号...
    computed: {
    	...mapState(['count','msg']);
    }
}
```



### Getter

store.js

```js
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex);

export default new Vuex.Store({
  state: {
    count: 0,
    msg: 'msg',
    list: [1, 2, 3, 4]
  },
  getters: {
    modifyArr(state) {
      return state.list.filter((item, index, arr) =>{
      	return item % 2 == 0;
      })
    }
  }
})
```

app.js

```js
export default {
  //方法一
 	 computed: {
     list() {
       return this.$store.getters.modifyArr;
     }
   }
  //方法二 : mapGetters
  computed: {
  	...mapGetters(['modifyArr'])
    ...mapGetters({getList:'modifyArr'})//指定别名
	}
}
```



### Mutation

> - 可以修改store里面的状态
>
> - 必须是**同步函数**
>
> - 最好在store中先初始化所需要的属性
>
> - 当需要添加属性时, 使用Vue.set(obj, 'newProp', 123)或用新的对象替换老对象
>
>   - ```js
>     mutation: {
>       addNewState(state, payload){
>         Vue.set(state, 'newProp', '添加一个新的值');
>         //另外一个种
>         this.replaceStae({...state, newProp: '添加一个新值! ' })
>       }
>     }
>     
>     methods: {
>       addNewProp() {
>         this.$store.commit('addNewState', {});
>       }
>       newMsg() {
>         return this.$store.state.newProp || '还没有添加新值';
>       }
>     }
>     ```

```js
import { mapMutation } from 'vuex'
methods: {
  add() {
    this.$store.commit('add');
  },
  reduce() {
    this.$store.commit('reduce');
  },
  loadAdd() {
    
    this.$store.commit('loadAdd', 100)
    this.$store.commit('loadAdd', {
    	extraCount: 100
    })//传输额外的参数
    
    this.$store.commit({
      type:'addLoad'
      extraCount: 100
    },{}) //将多个写在一个上                  
  },
    
  //mapMutation using
  ...mapMutations([
    'increment',//将`this.increment`映射为'this.$store.commit(increment)'
    'incrementBy',//将'this.incrementBy(amount)'映射为'this.$store.commit('incrementBy', amount)'
  ])
  // 取别名
  ...mapMutations([
    add: 'increment',
    get: 'incrementBy',
  ])
  
}

//store.js
mutations: {
  add(state) {
    state.count++;
  },
  reduce(state) {
    state.count--;
  },
  loadAdd(state, payload) {  // 提交载荷，额外参数
    state.count += payload;
  },
},


```



### Action

> - 可以自行异步操作,
> - 类似于Mutation
> - 不可以直接修改state



```js
actions: {
  changeProduct(context, payload) { // 这个context是一个与 store 实例具有相同方法和属性的对象
    // 调用mutation里的changeProduct方法
    // context.commit('changeProduct', {change: 'ship'});
    // 改成异步方式
    // setTimeout(() => {
    //   context.commit('changeProduct', {change: 'ship'});
    // }, 1500)
    // 使用载荷
    let temp = 'ship+' + payload.extraInfo; 
    setTimeout(() => {
      context.commit('changeProduct', {change: temp});
    }, 1500)
  }
}


methods: {
  selectProduct() {
    // this.$store.dispatch('changeProduct')
    // 载荷方式分发
    // this.$store.dispatch('changeProduct', {
    //   extraInfo: 'sportcar'
    // })
    // 或者这种
    this.$store.dispatch({
      type: 'changeProduct',
      extraInfo: '->sportcar'
    })
  }
},
```

利用Promise

```js
state: {
	userInfo: {
  	name: 'guan',
    age:23,
  }
},
mutation: {
	changeInfo(state, payload) {
    state.userInfo.name = 'ruihua'
  }
},
actions: {
	changeInfo(context, payload) {
    return new Promise( (resolve, reject) => {
      setTimeout(() => {
        context.commit('changeInfo');
        resolove();
      },2000)
    })
  }
}
  
//app.js
  
data() {
  return {
    status: 'no changed',
  }
},
methods: {
  modifyInfo() {
		this.$store.dispatch('changeInfo')
  }
}
```

action可以相互调用

```js
actions: {
  actionA ({ commit }) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        commit('someMutation')
        resolve()
      }, 1000)
    })
  },
  actionB ({ dispatch, commit }) {
    return dispatch('actionA').then(() => {//调用了actionA
      commit('someOtherMutation')
    })
  }
}

```







### Module

#### 分模块管理方法

```js
//先定义两个模块
const moduleA = {
	state: {
  	name: 'guan',
    age: '23'
  },
  mutations: {},
  getters: {},
  action: {},
}

const moduleB = {
	state: {
  	name: 'rui',
    age: '22'
  },
  mutations: {},
  getters: {},
  action: {},
}

//在Vuex里面声明模块
export default new Vuex.Store({
	modules: {
  	ma: moduleA,
    mb: moduleB
  },
  state: {
    ...//其他状态
  },
})
  
  
//app.vue
compute: {
	msg() {
		return this.$store.mb; //{name: 'rui', age: '22'}	
	}
}
```



#### 命名空间模块

```js
export const moduleC = {
  namespaced: true,
  state: {
    name: 'moduleC',
    desc: '这是模块C，用来测试命名空间的！',
    list: [1, 2, 3, 4]
  },
  getters: {
    filterList(state) {
      return state.list.filter((item, index, arrSelf) => {
        return item % 2 !== 0;
      });
    }
  },
  mutations: {
    modifyName(state, payload) {
      state.name = payload.newName;
    }
  },
  actions: {
    
  }
}
//store.js
import { moduleC } from './module_c.js';

export default new Vuex.Store({
  modules: {
    mc: moduleC
  },
})

methods: {
  modify() {
    // this.$store.commit('mc/modifyName', {
    //   newName: '命名空间模块C'
    // })
    this.$store.commit({
      type: 'mc/modifyName',
      newName: '命名空间模块C'
    })
  }
}


//命名空间发生改变后,mapState,mapGetters, mapMutations, mapActions用法改变
// 1.
...mapState('mc', ['name', 'age']);
...mapState('mc', {
	name(state) {
    return state.name;
  },
  age(state) {
    return state.age;
  }
})
// 2. 使用createNamespacedHelpers创建基于某个命名空间辅助函数
import { createNamespacedHelpers } from 'vuex';
const { mapState, mapMutations } = createNamespacedHelpers('mc');
```

## Vue-typeScript

### 环境搭建

```shell
vue create typescript-app & cd typescript-app & npm run serve
```

### Main

#### 基于类的组件

```typescript
//Typescript code
<script lang="ts">//这里指定是typescript
import { Component, Vue } from "vue-property-decorator"
@Component
export default class HelloWorld extends Vue {
  //coding...
}
//显式地使用name属性
@Component({
  name: 'HelloWorld',
})
</script>


//Javascript code
<script>
  export default {
	name: 'helloWorld',
}
</script> 
```

#### 引入组件

````javascript
//typescript
<template>
  <div class="main">
    <Project/>
  </div>
</template>
<script lang='ts'>
	import { Component, Vue } from 'vue-property-decorator'
	import Project from '@/components/Project.vue'
	@Component({
    commponents: {
      Project
    }
  })
export default class HelloWorld extends Vue{
  //coding...
}
</script>


//javascript
<template>
  <div class = "main">
    <Project/>
  </div>
</template>
<script>
  import Project from '@/components/Project.vue'
	export defaulf {
    name : 'HelloWordl',
    components : {
      Project
    }
  }	
</script>
````

#### Data, props, computed, methods, watchers, emit

##### Data

```javascript
//Typescript
@Component
export default class HelloWorld extends Vue{
  private msg : string = 'guanruihua'
	private list : Array<object> = [
    {
      name : 'ruihua',
      age : '23',
    },
    {
      name : 'ruihua', 
      age : '30',
    }
  ]
}

//javascript
export default {
  data(){
    return {
      msg : 'guanruihua',
      list : [
        {
          name : 'ruihau',
          age : '23',
        },
        {
          name : 'ruihua', 
          age : '30'
        }
      ]
    }
  }
}
```

##### props

```javascript
//typescript
import { Component, Prop, Vue } from 'vue-property-decorator'
@Component
export default class HelloWorld extends Vue {
  @Prop() readonly msg!:string
  @Prop({default : 'ruihua' }) readonly name : string
  @Prop({required: true }) readonly age : number
  @Prop(String) readonly address : string
  @Prop({ require: false, type: String, default: 'Developer'}) readonly job: string
}

//javascript
props:{
  msg,
  name: {
    default: 'ruihua'
  },
  age: {
  	require: true,
  },
  address: {
  	type: String
  },
  job: {
  	require: false,
    type: String,
    default: 'Developer'
  }
    
}
```

#### Computed

```javascript
//Typescript
export default class HelloWorld extends Vue {
	get fullName() :string {
		return this.firstName + '' + this.lastName
  }
	set fullName(newValue: string){
    let names = newValue.split(' ')
    this.firstName = names[0]
    this.lastName = names[ names.lenght - 1 ]
  }
}
//javascript
export default{
	fullName() {
  	return this.firstName + '' + this.lastName
  }
}

export default{
	fullName() {
    get: function(){
    	return this.firstName + '' + this.lastName  
    }
  	set: function( newValue ){
      let names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[ names.lenght - 1 ]
    }
  }
}
```

#### methods

```javascript
//Typescript
export default class HelloWorld extends Vue {
	public Fn() : void {
    console.log( this.addNum(4, 2) )
  }
	public addNum( num1: number, num2: number): number {
    return num1 + num2
  }
}

//javascript
export default {
  methods: {
  	Fn() {
    	console.log( this.addNum(4, 2))
    },
    addNum(num1, num2){
      return num1 + num2
    }
  }
}
```

#### wetchers

```javascript
//typescript
@Watch('name')//监听的变量名称
nameChange(newVal: string){
  this.name = newVal
}

@Watch('project', { 
  immediate: true, deep: true 
})
projectChanged(newVal: Person, oldVal: Person) {
  // do something
}
//javascript
watch: {
	person: {
  	handler: 'projectChanged',
		immediate: true,
     deep: true
  }
},
  methods:{
  	projectChanged:(new Val, oldVal){
      //do something
    }
  }
```

