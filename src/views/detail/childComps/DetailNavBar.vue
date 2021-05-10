<template>
  <div>
    <nav-bar>
      <div slot="center" class="center">
        <div v-for="(item, index) in titles"
             class="center-item"
             :class="{active: index === currentIndex}"
             @click="itemClick(index)">{{ item }}</div>
      </div>
    </nav-bar>
  </div>
</template>
<script>
import NavBar from "components/common/navbar/NavBar";
export default {
  name: "DetailNavBar",
  data() {
    return {
      titles: ["商品", "参数", "评论", "推介"],
      currentIndex: 0
    };
  },
  components: {
    NavBar,
  },
  methods: {
    itemClick(index) {
      this.currentIndex = index
    }
  }
};
</script>

<style scoped>
.center {
  display: flex;
  font-size: 13px;
}
.center-item {
  flex: 1;
}
.active{
  color: var(--color-high-text);
  border-bottom: 2px solid var(--color-tint);
}
</style>>
