<template>
  <div class="goods">
    <good-list-item v-for="item in goods" :goods-item="item"></good-list-item>
  </div>
</template>

<script>
import GoodListItem from "./GoodsListItem";
export default {
  name: "GoodList",
  components:{
    GoodListItem
  },
  props: {
    goods: {
      type: Array,
      default() {
        return []
      }
    },
  },
  methods: {}
};
</script>

<style>
  .goods {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
  }

</style>
