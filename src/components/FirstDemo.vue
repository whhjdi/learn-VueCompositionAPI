<template>
  <div>
    <h2>setup,reactive,ref</h2>
    <div>
      count is {{ count }},
      foo is {{ object.foo }},
    </div>
    <div>
      修改object里的count2的值为：{{object.count2}}
      此时count2的值也变为{{count2}}
    </div>
    <div>name-{{name}}</div>
    <div>count是否是ref:{{isref}}</div>
  </div>
</template>

<script>
import { ref, reactive, watch, isRef, toRefs } from "@vue/composition-api";

function useFeatureX() {
  const state = reactive({
    foo: 1,
    bar: 2
  });

  // logic operating on state

  // convert to refs when returning
  return toRefs(state);
}

export default {
  props: {
    name: String
  },
  setup(props) {
    const { foo, bar } = useFeatureX();
    console.log("foo:" + foo.value, "bar:" + bar.value);
    const count = ref(0);
    const count2 = ref(2);
    const object = reactive({ foo: "bar", count2 });
    const isref = isRef(count);
    console.log("count:" + count.value++);
    console.log("count+1:" + count.value);
    const state = reactive({
      foo: 1,
      bar: 2
    });
    object.count2 = 10;
    watch(() => {
      console.log(props.name);
    });

    const domRef = ref(null);
    // expose to template
    return {
      count,
      isref,
      count2,
      object
    };
  }
};
</script>
