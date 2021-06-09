<template>
  <div>Test Stepper</div>
  <Stepper />
</template>

<script>
import Stepper from "./Stepper.vue";
export default {
  name: "TestStepper",
  components: {
    Stepper,
  },
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>