<template>
  <div>
    Dummy component
    <div v-bind:key="val.id" v-for="val in valuess">
      <li>{{ val.name }}</li>
    </div>
  </div>
</template>

<script>
export default {
  name: "DummyComp",
  props: ['valuess'],

  created() {
    console.log("Dummy comp", this.valuess, typeof this.valuess);
  },
};
</script>