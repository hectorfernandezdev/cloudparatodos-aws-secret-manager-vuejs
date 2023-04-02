<template>
  <img
    alt="AWS UG Montevideo"
    src="https://d2rohywdd3ng4p.cloudfront.net/assets/images/sticker_general.png"
    class="logo-aws-ug-montevideo"
  />
  <HelloWorld msg="Welcome to Your Vue.js App" />
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
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
.logo-aws-ug-montevideo {
  max-width: 200px;
}
</style>
