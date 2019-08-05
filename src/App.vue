<template>
  <div id="app">
    <Calculator msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
  name: "app",
  components: {
    Calculator
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

html,
body {
  margin: 0;
  padding: 0;
  font-size: 16px;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  color: #2c3e50;
  display: grid;
  height: 100vh;
  border: 2px solid red;
  justify-items: center;
  align-items: center;
}

.calc-container {
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 100vw;
  background-color: yellow;
  justify-content: center;
  align-items: center;
}
</style>
