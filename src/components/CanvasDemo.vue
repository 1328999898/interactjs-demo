<template>
  <canvas :width="width" :height="height" ref="canvasDemo"></canvas>
</template>
<script>
import interact from 'interactjs'
export default {
  name: "ResizingDemo",
  data() {
    return {
      width: 100,
      height: 100
    }
  },
  mounted() {
    this.draw();
    // 当改变画布的大小时，画布会重绘，导致已经绘制好的画布内容消失
    this.width = 200;
    this.height = 200;
    setTimeout(() => {
      this.draw();
    }, 0);
  },
  methods: {
    draw() {
      const cs = this.$refs.canvasDemo;
      const ctx = cs.getContext('2d');
      ctx.fillStyle= '#ccc';
      ctx.fillRect(0, 0, this.width, this.height);      
    },
  },
}
</script>
<style scoped>
.resize-drag {
  width: 120px;
  border-radius: 8px;
  padding: 20px;
  margin: 1rem;
  background-color: #29e;
  color: white;
  font-size: 20px;
  font-family: sans-serif;
  touch-action: none;
  box-sizing: border-box;
}
</style>