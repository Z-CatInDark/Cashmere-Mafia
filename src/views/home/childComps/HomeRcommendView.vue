<template>
  <div class="home-recommend">
    <div class="home-recommend-item" v-for="item in recommend" >
      <a :href="item.link">
        <img :src="item.image" alt="">
        <div>{{item.title}}</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name:"HomeRcommendView",
  props:{
    recommend:{
      type:Array,
      default() {
        return []
      }
    }
  },
  methods: {
  }
}
</script>

<style>
  .home-recommend{
    display: flex;
    text-align: center;
    padding: 10px 0 10px;
    border-bottom: 10px solid #eee;
  }
  .home-recommend-item{
    flex: 1;
  }
  .home-recommend-item img{
    width: 85%;
    margin-bottom: 5px;
  }
</style>
