<template>
  <div>
    <tar-bar>
      <tar-bar-item path="/home" activeColor="deeppink">
        <!-- 动态替换TarBarItem里的插槽 -->
        <img
          slot="item-icon"
          src="~assets/img/tarbar/default/home.svg"
        />
        <img
          slot="item-icon-active"
          src="~assets/img/tarbar/active/home_active.svg"
        />
        <div slot="item-text">首页</div>
      </tar-bar-item>
      <tar-bar-item path="/category" activeColor="deeppink">
        <img
          slot="item-icon"
          src="~assets/img/tarbar/default/category.svg"
        />
        <img
          slot="item-icon-active"
          src="~assets/img/tarbar/active/category_active.svg"
        />
        <div slot="item-text">分类</div>
      </tar-bar-item>
      <tar-bar-item path="/shopcart" activeColor="deeppink">
        <img
          slot="item-icon"
          src="~assets/img/tarbar/default/shopcart.svg"
        />
        <img
          slot="item-icon-active"
          src="~assets/img/tarbar/active/shopcart_active.svg"
        />
        <div slot="item-text">购物车</div>
      </tar-bar-item>
      <tar-bar-item path="/profile" activeColor="deeppink">
        <img
          slot="item-icon"
          src="~assets/img/tarbar/default/profile.svg"
        />
        <img
          slot="item-icon-active"
          src="~assets/img/tarbar/active/profile_active.svg"
        />
        <div slot="item-text">我的</div>
      </tar-bar-item>
    </tar-bar>
  </div>
</template>

<script>
import TarBar from "components/common/tarbar/TarBar";
import TarBarItem from "components/common/tarbar/TarBarItem";
export default {
  name:'MinaTarBar',
  components:{
    TarBar,
    TarBarItem
  }
};
</script>

<style>
</style>
