<template>
  <h1>拖拽</h1>
  <div id="drag-1" class="draggable">
    <p>you can drag one element</p>
  </div>
  <div id="drag-2" class="draggable">
    <p>with each point</p>
  </div>
</template>
<script>
import interact from "interactjs";
export default {
  name: "DraggableDemo",
  data() {
    return {};
  },
  mounted() {
    interact(".draggable").draggable({
      // manualStart: true,
      // enable inertial throwing
      inertia: true,
      // keep the element within the area of it's parent
      modifiers: [
        interact.modifiers.restrictRect({
          restriction: "parent",
          endOnly: true
        })
      ],
      // enable autoScroll
      autoScroll: true,

      listeners: {
        start(event) {
          // 开始拖动
          console.log('start',event);
        },
        move(event) {
          // 移动事件
          console.log('move', event.x0,event.y0, event.dx, event.dy);

          var target = event.target;
          // 通过data-x/data-y属性，维护拖拽的位置
          var x = (parseFloat(target.getAttribute("data-x")) || 0) + event.dx;
          var y = (parseFloat(target.getAttribute("data-y")) || 0) + event.dy;

          // 移动位置
          target.style.webkitTransform = target.style.transform =
            "translate(" + x + "px, " + y + "px)";
          const { width, height } = event.rect;
          target.style['transform-origin'] = `${width / 2}px ${height / 2}px`;

          // 更新位置属性
          target.setAttribute("data-x", x);
          target.setAttribute("data-y", y);
          
        },
        end(event) {
          // 结束移动事件
          console.log("end", event);
        }
      }
    });
  }
};
</script>
<style scoped>
#drag-1,
#drag-2 {
  width: 25%;
  min-height: 6.5em;
  margin: 1rem 0 0 1rem;
  background-color: #29e;
  color: white;
  border-radius: 0.75em;
  padding: 4%;
  touch-action: none;
  user-select: none;
  -webkit-transform: translate(0px, 0px);
  transform: translate(0px, 0px);
}
</style>
