<template>
  <p>Comp 1: {{ name }}</p>
  <input v-model="name" />
</template>

<script>
export default {
  name: "comp1",
  data() {
    return { name: "" };
  },
};
</script>
