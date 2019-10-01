<template>
  <div class="home">
    <FirstDemo :name="obj.name" />
    <button @click="handleButton">改变props</button>

    <SecondDemo />
    <ThirdDemo></ThirdDemo>
  </div>
</template>

<script>
// @ is an alias to /src
import FirstDemo from "@/components/FirstDemo.vue";
import SecondDemo from "@/components/SecondDemo.vue";
import ThirdDemo from "@/components/ThirdDemo.vue";
import { reactive } from "@vue/composition-api";
export default {
  name: "home",
  components: {
    FirstDemo,
    SecondDemo,
    ThirdDemo
  },
  setup() {
    function handleButton(e) {
      obj.name = "小明";
    }
    const obj = reactive({ name: "muxue" });
    return {
      obj,
      handleButton
    };
  }
};
</script>
