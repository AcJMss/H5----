<!--
 * @Author: chenjm
 * @Date: 2022-09-21 11:18:50
 * @LastEditors: chenjm
 * @LastEditTime: 2022-09-21 13:34:58
 * @Description: 
-->
<template>
  <h5-sign />
</template>

<script>
import h5Sign from "./components/h5Sign.vue";

export default {
  name: "App",
  components: {
    h5Sign
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
