<template>
  <div ref="root">
    <h2>watch,lifeCycle,remplate refs,v-for....</h2>
    <div>{{state.count}}</div>
    <div>{{name}}</div>
    <ul>
      <li v-for="(item,index) in list" :ref="el=>{divs[i]=el}">{{item}}</li>
    </ul>
  </div>
</template>

<script>
import {
  ref,
  reactive,
  watch,
  isRef,
  toRefs,
  computed,
  onMounted,
  onUpdated,
  onUnmounted,
  onBeforeUpdate
} from "@vue/composition-api";

export default {
  setup() {
    const root = ref(null);
    onMounted(() => {
      console.log("mounted!");
      console.log(root.value);
    });
    onUpdated(() => {
      console.log("updated!");
    });
    onUnmounted(() => {
      console.log("unmounted!");
    });
    const state = reactive({ count: 0, age: 16 });
    const name = ref("我的名字是🦑");
    const stop = watch(() => state.age);
    console.log("开始监听age");
    setTimeout(() => {
      stop();
      console.log("停止监听age");
    }, 3000);

    watch(
      () => state.count,
      (count, prevVal) => {
        console.log("监听state的count：" + count, prevVal);
      }
    );
    watch(name, (name, prevVal) => {
      // 这个name不需要name.value
      console.log("监听ref,name:" + name, prevVal);
    });
    //     watch([fooRef, barRef], ([foo, bar], [prevFoo, prevBar]) => {
    //   /* ... */
    // })

    const list = reactive([1, 2, 3, 4, 5]);
    const divs = ref([]);
    onBeforeUpdate(() => {
      divs.value = [];
    });
    return {
      state,
      name,
      root,
      list,
      divs
    };
  }
};
</script>
