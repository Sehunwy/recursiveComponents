<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
/* eslint-disable */
import iconfont from "@/assets/js/iconfont.js";
import { allModule } from "@/lib/config.js";
import Router from "vue-router";
export default {
  name: "App",
  data() {
    return {
      modules: [],
      route: []
    };
  },
  created() {
    allModule.then(result => {
      this.modules = result;
    });
  },
  watch: {
    modules: function(newVal, oldVal) {
      for (var i = 0; i < newVal.length; i++) {
        this.$router.options.routes.push(newVal[i].getMenu());
      }
      this.$router.addRoutes(this.$router.options.routes);
    }
  }
};
</script>

<style>
/* #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
body,
html {
  margin: 0px;
  padding: 0px;
  height: 100%;
  width: 100%;
  color: #333333;
  font-size: 14px;
}

.icon {
  width: 1em;
  height: 1em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
}

#app {
  width: 100%;
  height: 100%;
  background-color: #e9ecef;
}

ul,
li,
ol {
  list-style: none;
}

p,
ul,
li,
ol {
  margin: 0px;
  padding: 0px;
}
</style>
