<template>
  <p>Comp 2: {{ name }}</p>
  <input v-model="name" />
</template>

<script>
export default {
  name: "comp2",
  data() {
    return { name: "" };
  },
};
</script>
