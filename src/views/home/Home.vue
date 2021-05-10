<template>
  <div id="home">
    <nav-bar class="home-nav-bar"><span slot="center">女人世界</span></nav-bar>
    <tab-control
      ref="tabControl1"
      :titles="['流行', '新款', '精选']"
      @tabItemClick="tabClick"
      class="tab-control"
      v-show="isOffsetTop"
    ></tab-control>
    <scroll
      class="content"
      ref="scroll"
      @scroll="getPostion"
      :probe-type="3"
      :pull-up-load="true"
      @pullUpLoad="loadMore"
    >
      <home-swiper :banners="banners" @imgload="swiperImgLoad"></home-swiper>
      <home-rcommend-view :recommend="recommend"></home-rcommend-view>
      <home-feature-view></home-feature-view>
      <tab-control
        ref="tabControl2"
        :titles="['流行', '新款', '精选']"
        @tabItemClick="tabClick"
      ></tab-control>
      <good-list :goods="showGoods"></good-list>
    </scroll>
    <back-top @click.native="backTopClick" v-show="isShowBackTop"></back-top>
  </div>
</template>

<script>
import HomeSwiper from "./childComps/HomeSwiper";
import HomeRcommendView from "./childComps/HomeRcommendView";
import HomeFeatureView from "./childComps/HomeFeatureView";

import Scroll from "components/common/scroll/Scroll";
import NavBar from "components/common/navbar/NavBar";
import TabControl from "components/content/tabControl/TabControl";
import GoodList from "components/content/goods/GoodsList";
import BackTop from "components/content/backTob/BackTop";

import { getHomeMultideta, getHomeGoodsData } from "network/home";
import { debounce } from "common/utils.js";
export default {
  name: "Home",
  data() {
    return {
      banners: [],
      recommend: [],
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] },
      },
      currentType: "pop",
      isShowBackTop: false,
      tabOffsetTop: 0,
      isOffsetTop: false,
      saveY: 0
    };
  },
  components: {
    HomeSwiper,
    HomeRcommendView,
    HomeFeatureView,

    Scroll,
    NavBar,
    TabControl,
    GoodList,
    BackTop,
  },
    activated() {
      this.$refs.scroll.scroll.scrollTo(0, this.saveY, 0)
      this.$refs.scroll.refresh()
    },
    deactivated() {
      this.saveY = this.$refs.scroll.getScrollY()
    },
  created() {
    // 获取轮播图数据
    this.getHomeMultideta();
    // 获取首
    this.getHomeGoodsData("pop");
    this.getHomeGoodsData("new");
    this.getHomeGoodsData("sell");
  },
  mounted() {
    const refresh = debounce(this.$refs.scroll.refresh, 300);
    this.$bus.$on("itemimgload", () => {
      refresh();
    });
  },
  computed: {
    showGoods() {
      return this.goods[this.currentType].list;
    },
  },
  methods: {
    tabClick(index) {
      switch (index) {
        case 0:
          this.currentType = "pop";
          break;
        case 1:
          this.currentType = "new";
          break;
        case 2:
          this.currentType = "sell";
          break;
      }
      this.$refs.tabControl1.currentIndex = index;
      this.$refs.tabControl2.currentIndex = index;
    },
    swiperImgLoad() {
      this.tabOffsetTop = this.$refs.tabControl2.$el.offsetTop;
    },
    loadMore() {
      this.getHomeGoodsData(this.currentType);
    },
    backTopClick() {
      this.$refs.scroll.backClick(0, 0, 300);
    },
    getPostion(postion) {
      this.isShowBackTop = -postion.y > 200;
      this.isOffsetTop = -postion.y > this.tabOffsetTop;
    },

    // 网络请求
    getHomeMultideta() {
      getHomeMultideta().then((res) => {
        this.banners = res.banner.list;
        this.recommend = res.recommend.list;
      });
    },
    getHomeGoodsData(type) {
      const page = this.goods[type].page + 1;
      getHomeGoodsData(type, page).then((res) => {
        this.goods[type].list.push(...res.list);
        this.goods[type].page += 1;
        this.$refs.scroll && this.$refs.scroll.finishPullUp();
      });
    },
  },
};
</script>

<style scoped>
#home {
  height: 100vh;
  position: relative;
}

.home-nav-bar {
  background-color: var(--color-tint);
  color: #fff;
}
.content {
  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
  right: 0;
  left: 0;
}
.tab-control {
  position: relative;
  z-index: 9;
}
</style>
