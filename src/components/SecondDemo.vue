<template>
  <div>
    <h2>computed</h2>
    <div>plusOne is {{plusOne}}</div>
    <div>plusTwo : {{count2}}+ 2 = {{plusTwo}}</div>
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
  readonly
} from "@vue/composition-api";

export default {
  setup() {
    const count1 = ref(0);
    const count2 = ref(1);
    const plusOne = computed(() => count1.value + 1);
    const plusTwo = computed({
      get: () => {
        return count2.value;
      },
      set: val => {
        return (count2.value = val + 2);
      }
    });
    console.log((plusTwo.value = 10));
    const original = reactive({ origin: 1 });
    console.log("r" + readonly);
    // const copy = readonly(original);
    return {
      plusOne,
      count2,
      plusTwo
    };
  }
};
</script>
