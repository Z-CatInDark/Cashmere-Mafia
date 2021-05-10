<template>
  <div class="tar-bar-item" @click="itemClick">
    <!-- 将文字和图片放到APP组件里插入 -->
    <div v-if="!isActive"><slot name="item-icon"></slot></div>
    <div v-else><slot name="item-icon-active"></slot></div>
    <!-- 用v-bind绑定class，当isActuve为true时绑定添加class属性名，为false时去除达到动态绑定的目的 -->
    <div :style="activeStyle"><slot name="item-text"></slot></div>
  </div>
</template>

<script>
export default {
  name: "TarBarItem",
  props:{
    /*
      父子组件通讯运用
      1，在父组件中将点击的路径赋值给path属性，在子组件中在props对象中同时定义一个path拿到父组件中的值
      2. 可以对定义的属性进行一些操作，比如指定数据类型和设置默认值
    */
    path: String,
    activeColor:{
      type: String,
      default: 'red'
    }
  },
  data() {
    return {
      // isActive: true,
    };
  },
  computed:{
    isActive() {
      /*
        动态判断组件是否处于激活状态
        1.判断当前处于活跃的route里的path属性是否等于我们点击时传入的path属性
        2.如果能等于则不等于-1返回值为true
        3.找不到返回值则为false

      */
      return this.$route.path.indexOf(this.path) !== -1
    },
    activeStyle() {
      // isActive？ 当isActive处于活跃时执行 ：不处于活跃时执行
      return this.isActive ? {color: this.activeColor} : {}
    }
  },
  methods:{
    itemClick() {
      // 跳转到获取的path路径
      this.$router.replace(this.path)
    }
  }
};
</script>

<style>
  /* 这个样式导入后会与外层样式合并所以fix布局能起作用 */
  .tar-bar-item {
    flex: 1px;
    text-align: center;
    height: 49px;
    font-size: 14px;
  }
  .tar-bar-item img {
    width: 24px;
    height: 24px;
    /* 外边距 */
    margin-top: 3px;
    margin-bottom: 2px;
    /* 消除图默认的下边距3px */
    vertical-align: middle;
  }
  /* 文字样式动态绑定 */
  /* .active {
    color: deeppink;
  } */
</style>
