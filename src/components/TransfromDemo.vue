<template>
  <div class="f-content">
    <div class="s-content">
    

    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {

    }
  }
}
</script>
<style scoped>
.f-content {
  width: 200px;
  height: 200px;
  -webkit-transform: translate(0, 0);
  transform: translate(0, 0);
  border: 1px solid #666;
}
.s-content {
  width: 100px;
  height: 100px;
  border: 1px solid blue;
  transform: scale(0.5) translate(100px);
  transform-origin: bottom right;
}
</style>