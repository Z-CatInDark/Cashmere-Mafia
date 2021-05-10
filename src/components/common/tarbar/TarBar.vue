<template>
  <div>
    <div id="tar-bar">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "TarBar",
};
</script>

<style>
#tar-bar {
  display: flex;
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  box-shadow: 0 -1px 1px rgba(100, 100, 100, 0.1);
  background-color: #fff;
}
</style>
