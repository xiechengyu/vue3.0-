<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" />
  <div> -->
  <!-- <h2>欢迎光临红浪漫洗浴中心</h2>
    <div>请选择一位美女为你服务</div> -->
  <!-- </div>
  <div>
    <button
      v-for="(item, index) in girls"
      :key="index"
      @click="selectGirlFun(index)"
    >
      {{ index }} : {{ item }}
    </button>
  </div>
  <div>你选择了【{{ selectGirl }}】为你服务</div>
  <div><button @click="overAction">点餐完毕</button></div>
  <div>{{ overText }}</div> -->
  <!-- <div>{{ nowTime }}</div>
  <div><button @click="getNowTime">显示时间</button></div>
  <h2>欢迎光临红浪漫洗浴中心</h2>
  <div>随机选择一位美女为你服务</div>
  <div v-if="loading">Loading.....</div>
  <img v-if="loaded" :src="result.message" /> -->
  <div></div>
  <!-- <modal /> -->
  <!-- <teleport to="#modal">
    <div id="center">
      <h2>JSPang11</h2>
    </div>
  </teleport> -->

  <!-- 第一个default代表异步请求完成后，显示的模板内容。fallback代表在加载中时，显示的模板内容。 -->
  <!-- <Suspense>
    <template #default>
      <AsyncShow />
    </template>
    <template #fallback>
      <h1>Loading...</h1>
    </template>
  </Suspense> -->
  <Suspense>
    <template #default>
      <GirlShow />
    </template>
    <template #fallback>
      <h1>Loading...</h1>
    </template>
  </Suspense>
</template>

<script lang="ts">
/**
 *  
1、setup 函数的用法，可以代替 Vue2 中的 date 和 methods 属性，直接把逻辑卸载 setup 里就可以
ref 函数的使用，它是一个神奇的函数，我们这节只是初次相遇，要在template中使用的变量，必须用ref包装一下。
return出去的数据和方法，在模板中才可以使用，这样可以精准的控制暴漏的变量和方法。

2、reactive。它也是一个函数(方法)，只不过里边接受的参数是一个 Object(对象)

3、interface)来作类型注解

4、toRefs把 data 变成refData,这样就可以使用扩展运算符的方式了

5.setup() :开始创建组件之前，在beforeCreate和created之前执行。创建的是data和method
onBeforeMount() : 组件挂载到节点上之前执行的函数。
onMounted() : 组件挂载完成后执行的函数。
onBeforeUpdate(): 组件更新之前执行的函数。
onUpdated(): 组件更新完成之后执行的函数。
onBeforeUnmount(): 组件卸载之前执行的函数。
onUnmounted(): 组件卸载完成后执行的函数
onActivated(): 被包含在<keep-alive>中的组件，会多出两个生命周期钩子函数。被激活时执行。
onDeactivated(): 比如从 A 组件，切换到 B 组件，A 组件消失时执行。
onErrorCaptured(): 当捕获一个来自子孙组件的异常时激活钩子函数（以后用到再讲，不好展现）。

6.
Vue2--------------vue3
beforeCreate  -> setup()
created       -> setup()
beforeMount   -> onBeforeMount
mounted       -> onMounted
beforeUpdate  -> onBeforeUpdate
updated       -> onUpdated
beforeDestroy -> onBeforeUnmount
destroyed     -> onUnmounted
activated     -> onActivated
deactivated   -> onDeactivated
errorCaptured -> onErrorCaptured

7.onRenderTracked和onRenderTriggered用来调试

8.watch

9.直接引用模块代替mixins引入

10.封装axios

11.teleport把组件渲染到你任意想渲染的外部Dom上

12.，Suspense提供两个template的位置，一个是没有请求回来时显示的内容，一个是全部请求完毕的内容。这样进行异步内容的渲染就会非常简单。
    返回一个promise对象

13.onErrorCaptured捕获异常
 */
import {
  // ref,
  // reactive,
  // toRefs,
  // onMounted,
  // onBeforeMount,
  // onBeforeUpdate,
  // onUpdated,
  // onRenderTracked,
  // onRenderTriggered,
  // watch,
  onErrorCaptured,
} from "vue";
// interface DataProps {
//   girls: string[];
//   selectGirl: string;
//   selectGirlFun: (index: number) => void;
// }
import { nowTime, getNowTime } from "./hooks/useNowTime";
import useUrlAxios from "./hooks/useUrlAxios";
// import modal from "./components/Modal.vue";
// import AsyncShow from "./components/AsyncShow.vue";
import GirlShow from "./components/GirlShow.vue";

export default {
  name: "App",
  components: {
    // modal,
    // AsyncShow,
    GirlShow,
  },
  setup() {
    // console.log("1-开始创建组件-----setup()");
    // const data: DataProps = reactive({
    //   girls: ["大脚", "刘英", "晓红"],
    //   selectGirl: "",
    //   selectGirlFun: (index: number) => {
    //     data.selectGirl = data.girls[index];
    //   },
    // });
    // const refData = toRefs(data);
    // const overText = ref("红浪漫");
    // const overAction = () => {
    //   overText.value += "点餐成功";
    //   document.title = overText.value;
    // };
    // watch([overText, () => data.selectGirl], (newValue, oldValue) => {
    //   console.log(`new--->${newValue}`);
    //   console.log(`old--->${oldValue}`);
    //   // document.title = newValue[0];
    // });
    // const { result, loading, loaded, error } = useUrlAxios(
    //   "https://dog.ceo/api/breeds/image/random"
    // );
    onErrorCaptured((error) => {
      console.log(`error====>`, error);
      return true;
    });
    return {
      // ...refData,
      // overText,
      // overAction,
      nowTime,
      getNowTime,
      // result,
      // loading,
      // loaded,
      // error,
    };
  },
};
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
