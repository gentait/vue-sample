<template>
  <div>
    <div class="header">へっだー</div>
    <div class="headerSpace"></div>
  </div>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
.header {
  position: fixed;
  width: 100%;
  height: 100px;
  font-size: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: gray;
}
.headerSpace {
  width: 100%;
  height: 100px;
}
</style>