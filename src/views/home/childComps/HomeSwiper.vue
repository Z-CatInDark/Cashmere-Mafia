<template>
  <swiper>
      <swiper-item v-for="item in banners">
        <a :src="item.link">
          <img :src="item.image" @load="imgload">
        </a>
      </swiper-item>
    </swiper>
</template>

<script>
import {Swiper, SwiperItem} from "components/common/swiper/index.js"
export default {
  name:"HomeSwiper",
  props: {
    banners: {
      type: Array,
      default() {
        return []
      }
    }
  },
  components: {
    Swiper,
    SwiperItem
  },
  data() {
    return {
      islaod: false
    }
  },
  methods: {
    imgload() {
      if (!this.islaod)
      this.$emit('imgload')
      this.islaod = true
    }
  }
}
</script>

<style>

</style>
