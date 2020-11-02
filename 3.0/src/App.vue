<template>
<img alt="Vue logo" src="./assets/logo.png">
<HelloWorld msg="Welcome to Your Vue.js App" />
</template>

<script>
import {
  reactive,
  toRefs,
  computed
} from 'vue' //下面的可以换成是这一种
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  setup() {
    const state = reactive({
      title: 'hello vue 3.0',
      age: 20,
      sex: '男',
      num: computed(() => 100) //计算属性的方法写法
    })
    //方法，要有返回值才会显示
    let dian = () => {
      state.age += 10;
      console.log(state.age);
    }
    // return state//返回全部的数据
    // return {//返回指定的数据
    //   title:state.title,
    //   age:state.age
    // }
    return {
      ...toRefs(state), //torefs响应式的方法，视图更新
      dian //导出方法，否则视图不更新
    }

  }
  // data () {//vue2.0的初始化数据
  //   return{
  //     aa:"hello"
  //   }
  // },
  // methods:{//方法属性
  //   ac(){
  //       let a='bb';
  //       this.aa=a;
  //   }
  // }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
