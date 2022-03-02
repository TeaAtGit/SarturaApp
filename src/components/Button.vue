<template>
  <button @click="click">{{ title }}</button>
</template>

<script>
export default {
  name: "Button",
  props: ["title", "click"],
};
</script>

<style scoped>
button {
  height: 48px;
  width: 100px;
  background: rgb(14, 65, 160);
  color: white;
  border: 0;
  border-radius: 4px;
  text-transform: uppercase;
  float: right;
  margin-top: 8px;
  margin-right: 8px;
}

button:hover {
  background: rgb(56, 102, 187);
  cursor: pointer;
}
</style>
