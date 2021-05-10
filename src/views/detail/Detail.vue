<template>
  <div id="detail">
    <detail-nav-bar></detail-nav-bar>
  </div>
</template>
vue
<script>
import DetailNavBar from "./childComps/DetailNavBar"
export default {
  name: "Detail",
  data() {
    return {
      iid: null
    }
  },
  created() {
    this.iid = this.$route.params.id
  },
  components: {
    DetailNavBar
  }
}
</script>

<style scoped>

</style>
