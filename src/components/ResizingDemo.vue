<template>
  <div class="resize-drag">
    Resize from any edge or corner
  </div>
</template>
<script>
import interact from 'interactjs'
export default {
  name: "ResizingDemo",
  mounted() {
    interact('.resize-drag')
    .on('tap', function(event) {
      console.log('单击')
      event.preventDefault();
    })
    .on('doubletap', function(event) {
      console.log('双击');
      event.preventDefault();
    })
    // 改变大小
    .resizable({
      edges: {
        left: true,
        right: true,
        bottom: true,
        top: true,
      },
      listeners: {
        move(event) {
          var target = event.target;
          var x = (parseFloat(target.getAttribute('data-x')) || 0);
          var y = (parseFloat(target.getAttribute('data-y')) || 0);
          console.log('rect', event.rect, event.deltaRect)
          x += event.deltaRect.left;
          y += event.deltaRect.top;

          target.style.width = event.rect.width + 'px';
          target.style.height = event.rect.height + 'px';
          target.style.webkitTransform = target.style.transfrom = `translate(${x}px, ${y}px)`;
          target.style['transform-origin'] = 'top';

          target.setAttribute('data-x', x);
          target.setAttribute('data-y', y);
        }
      },
      modifiers: [
        // 控制最小宽度 100、最小高度 100
        interact.modifiers.restrictSize({
          min: { width: 100, height: 100 }
        }),
        interact.modifiers.aspectRatio({
          ratio: 'preserve',
        })
      ]
    })
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

  /* This makes things *much* easier */
  box-sizing: border-box;
  /* 当resize的同时设置了缩放，interact会有bug */
  /* 解决方案：https://github.com/taye/interact.js/issues/430 */
  transform: scale(0.5); 
  transform-origin: 0px 0px; 
}
</style>