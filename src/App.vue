<template>
  <div id="app">
    <button @click="click1">点击基础1</button>
    <button @click="click2">点击基础2</button>
    <button @click="click3">点击高级1</button>
    <div >
      <test1 v-if="base1"></test1>
      <test2 v-if="base1"></test2>

      <async1  v-if="base2"></async1>
      <async2  v-if="base2"></async2>
      <async3  v-if="base2"></async3>

      <high1 v-if="high1"></high1>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import TxVueLoading from './tx-vue-loading'
import PageNotFound from './pageNotFound'
/**
 * 注意组件如果使用 v-show还是会按照异步规则加载，但是v-if则文件不会加载,等到点击之后，相应的组件才会按异步的形式加载组件，
 * 因为v-show只是样式设置为none,资源还是用了
 * 而 v-if根本就不去渲染，所以根本就没有用，所以资源也就不会加载了
 */
/**
 * 第一种，全局注册组件（当然能够在components中使用的语法也是可以在全局注册组件中使用的） ,传递函数进行一步加载 这里有个函数传递的参数为 resolve reject
 */
let test1 = Vue.component('test1',(resolve, reject) => {
              setTimeout(() => {
                return resolve({template: '<div>this is test1</div>'})
              },1000)
            })
let test2 = Vue.component('test2',(resolve, reject) => {
              setTimeout(() => {
                return resolve({template: '<p>this is test2</p>'})
              },2000)
            })

export default {
  name: 'app',
  data () {
    return {
      base1: false,
      base2: false,
      high1: false,
    }
  },
  components:{
    test1,
    test2,
    async1: (resolve,reject) =>{ //第二种 ，在组件中使用 写法一
      setTimeout(() => {
         resolve(require('./async1')) //直接require 不会被单独打包
      }, 3000);
    },
    async2: (resolve,reject) =>{// 写法二，将异步组件和 webpack 的 code-splitting 功能 ,require会把文件单独打包
      setTimeout(() => {
        return  require(['./async2'],resolve)
      }, 4000);
    },
    async3: () => import('./async3.vue'),//第三种写法和require(['./async2'],resolve) 一样，都会被单独打包 需要下载插件 babel-plugin-syntax-dynamic-import 然后在.babelrc文件加入 "plugins": ["syntax-dynamic-import"]
    high1: () => ({ //高级异步组件，但是这里有个问题，设置了delay 组件的加载没有延迟
      component: import('./high1.vue'),
      loading: TxVueLoading,
      error: PageNotFound,
      delay: 100,
      timeout: 5000
    })
  },
  methods: {
    //普通加载1
    click1() {
      this.base1 = !this.base1;
    },
    //普通加载1
    click2() {
      this.base2 = !this.base2;
    },
    //高级加载
    click3() {
      this.high1 = !this.high1;
    },
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


</style>
