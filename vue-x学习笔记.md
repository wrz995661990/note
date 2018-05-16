# Vuex指南
  ## 一个专为vue.js应用程序开发的状态管理模式
  
  ## 首先看一下它的项目结构
  
   ![项目结构](./图片1.png)
  
  - **初步使用**
    - 引入vuex并安装   import Vuex from ‘vuex’； Vue.use(Vuex)  
    - 创建store       let store  =  new  Vuex.Store({…});
    - 将store注入我们的vue实例中
    - 至此，所有的vue组件就可以访问我们的store实例了
     ***
  - **创建store的配置项-基本**
    - state – store的状态，用于存储集中管理的数据  
    - getters – 对state中的数据进行派生，类似于vue组件中的computed；
    - mutations – 用于改变状态（state中的数据），唯一改变状态的方式
    - actions  -   可包含任何操作
     ***
  - **store实例的方式和属性**
    - store中的state可以直接读取属性的状态
    - store中的getters可以获取各个getters项
    - store的commit方法可以提交mutations中的各项
    - store的dispatch方法可以触发actions中的各项
     ***
  - **getters中的函数**
    - Getters中的函数可以接收两个参数
    - 第一个参数为状态 state
    - 第二个参数为getters
    - 可以返回任何值，包括函数
    - 把getters理解为属性，类似于computed
    - getters是响应式的；
    - getters的作用是派生state的数据
     ***
  - **mutations中的函数**
    - mutations中的函数是唯一改变state的方式；
    - mutations中的函数接收两个参数
    - 第一个参数是状态(state)；
    - 第二个参数是用户提交的载荷（可以是任意的数据形式）
    - mutations必须是同步的且是纯函数
    - mutations中的函数应该由commit方法触发
     ***
  - **actions中的函数**
    - actions中的函数可以处理任何的事情（包括异步和提交mutations）
    - actions中的函数接收两个参数
    - 第一个参数是一个和store拥有同样属性方法的对象
    - 第二个参数是用户提交的载荷(可以是任意形式的数据)
    - actions中的函数必须通过dispatch方法触发
    ***
  - **组合action**
    - 理解了诸多action的特性之后，我们可以把多个action组合起来，在组合action之前需要知道dispatch这个函数的更多       功能；dispatch不仅能触发actions，还能返回一个promise，并且该promise是actions函数返回的promise；因此       我们可以组合actions（把多个异步函数组合在一起，处理继发或者并发的任务）；
      也可以结合 async/await函数
      ***
  - **认识vuex的数据流向图**
    ![流向图](./图片2.png)
    ***
  - **store实例的subscribe方法**
    - 该方法用于注册一个监听器，用来监听mutations被提交；所有的监听器都接收两个参数，第一个参数用于描述               mutations的动作；第二个参数是最新的状态（state）
      store.subscribe((mutation,state)=>{
	    console.log(mutation,state);	
      })
    ***
  - **辅助函数**
    - 为了在组件中方便使用vuex中的各项，vuex给我们提供了一些辅助函数，这些函数的作用就是把各项映射到组件中；

      辅助函数如下：
      mapState
      mapGetters
      mapMutations
      mapActions
    ***
  - **mapState**
    - 把状态的各项映射的组件中（三种写法）
    - 数组的形式  mapState([‘key1’,’key2’…])
    - 对象的形式  mapState({com:’vuex’})
    - 对象的函数形式  mapState({com(state){}})
    - 该函数返回一个对象，该对象为映射后键值的组合
    ***
  - **mapGetters,mapMutations,mapActions**
    - 映射各项到组件中（两种写法）
    - mapGetters/mapMutations/mapActions([‘key1’,’key2’…])
    - mapGetters/mapMutations/mapActions({key:’vuex’…})
    ***
  - **插件**
    - 创建实例时可接受 plugins作为参数
    - 该参数是一个数组，数组中是一个个的函数，这些函数就是插件
    - 每个插件都接收一个store作为参数
    - 插件在实例创建后被调用一次
    - 可以结合subscribe方法去监听mutations的变化
    - 使用vuex内置Logger插件  import createLogger from ‘vuex/dist/logger’
    ***
  - **模块**
    - store可以接受modules配置项,用来将状态树进行拆分
    - modules是个对象内配置的是各个子模块，子模块也包括state,getters,mutations,actions四项，可嵌套
    - 子模块中的state挂在各模块命名的对象下
    - 子模块中的其他三项直接暴露在根状态下
    - getters可以通过第三个参数接受根状态
    - actions通过rootState属性接受根状态
    ***
  - **模块-命名空间**
    - 可在模块中使用namespaced：true使该模块的名字可用；
    - 因为state本来就是嵌套的，所以对它没有影响
    - 辅助函数可以接收一个参数用来表示命名上下文环境
    - 可以通过createNamespacedHelpers(‘命名路径’)创建基于该命名空间的辅助函数
    - Store创建后可使用store.registerModule(‘命名’/[‘命名1’,’命名2’],{})注册模块
    ***
    
   # 下面是vuex的工作流程
      ```
      收先在视图通过commit发送commit指令执行mutations里面的方法（唯一通道）如果方法里设计异步的话就需要通过
      
      actions里面的方法发送（actions里面接受store作为参数，也是发送commit指令actions通过dispatch触发然后修
      
      改数据因为是响应式的所以状态改变后视图也会跟着改变 getters是state的派生（不会改变state状态）但是也是响应式的
      ```
   ***
    
     
    
    