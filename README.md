# 包上一层自定义 name 的壳

给 `keep-alive` 下的 `component` 接受的组件包上一层自定义 name 的壳。

```html
<script>
  import { h } from "vue";
  import comp1 from "./Comp1.vue";
  import comp2 from "./Comp2.vue";

  const comps = {
    comp1: comp1,
    comp111: comp1,
    comp2: comp2,
  };
  const wrappers = new Map();

  export default {
    data() {
      return { name: "comp1" };
    },
    methods: {
      getWrapper(name) {
        const wrapperName = "wrapper-" + name;
        let wrapper;
        if (wrappers.has(wrapperName)) {
          wrapper = wrappers.get(wrapperName);
        } else {
          wrapper = {
            name: wrapperName,
            render() {
              return this.$slots.default();
            },
          };
          wrappers.set(wrapperName, wrapper);
        }
        return wrapper;
      },
      wrap(name) {
        const wrapper = this.getWrapper(name);
        const component = comps[name];
        return h(wrapper, null, () => h(component));
      },
    },
  };
</script>

<template>
  <h2>包上一层自定义name的壳</h2>
  <button @click="name = 'comp1'">切换comp1</button>
  <button @click="name = 'comp111'">切换comp111</button>
  <button @click="name = 'comp2'">切换comp2</button>
  <p>Selected: {{ name }}</p>
  <hr />
  <keep-alive :include="['wrapper-comp1', 'wrapper-comp111']">
    <component :is="wrap(name)" />
  </keep-alive>
</template>
```
