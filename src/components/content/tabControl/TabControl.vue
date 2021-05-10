<template>
  <div class="tab-control">
    <div v-for="(item, index) in titles"
         class="tab-control-item"
         @click="tabItemClick(index)">
      <span :class="{active:index === currentIndex}">{{ item }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabControl",
  props: {
    titles: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data(){
    return{
      currentIndex: 0
    }
  },
  methods:{
    tabItemClick(index){
      this.currentIndex = index
      this.$emit('tabItemClick', index)
    }
  }
};
</script>

<style>
.tab-control {
  display: flex;
  text-align: center;
  font-size: 15px;
  height: 40px;
  line-height: 40px;
  background: #fff;
}
.tab-control-item {
  flex: 1;
}
.tab-control-item span{
  padding: 5px;
}
.active{
  color: var(--color-high-text);
  border-bottom: 2px solid var(--color-tint);
}
</style>
