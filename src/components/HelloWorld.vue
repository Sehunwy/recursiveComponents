<template>
  <div style="height: 100%;width: 100%;">
    <parentSider></parentSider>
  </div>
</template>

<script>
/* eslint-disable */
import parentSider from "@/components/siderBar/parentSider";
export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "Welcome to Your Vue.js App"
    };
  },
  components: {
    parentSider
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
