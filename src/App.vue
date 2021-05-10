<template>
  <div id="app">
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
    <mina-tar-bar></mina-tar-bar>
  </div>
</template>

<script>
import MinaTarBar from "components/content/minatarbar/MinaTarBar";
export default {
  name: "App",
  components: {
    MinaTarBar,
  },
};
</script>

<style>
@import "assets/css/base.css";
</style>
