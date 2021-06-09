<template>
  <div>
    <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <TestStepper />
    <hr />
    <TestTransferList />
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import TestTransferList from "./components/transferList/TestTransferList.vue";
import TestStepper from "./components/Stepper/TestStepper.vue";

export default {
  name: "App",
  components: {
    // HelloWorld,
    TestTransferList,
    TestStepper,
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
