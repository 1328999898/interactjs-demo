<template>
  <p>基本用法</p>
  <canvas class="rainbow-pixel-canvas"></canvas>
  <p>Drag to Draw, Double tag to Clear!</p>
</template>
<script>
import interact from 'interactjs'
export default {
  name: 'BaseDemo',
  props: {
    msg: String
  },
  data() {
    return {
      count: 0
    }
  },
  mounted() {
    var pixelSize = 16

    interact('.rainbow-pixel-canvas')
      .draggable({
        max: Infinity,
        maxPerElement: Infinity,
        origin: 'self',
        modifiers: [
          interact.modifiers.snap({
            // snap to the corners of a grid
            targets: [
              interact.snappers.grid({ x: pixelSize, y: pixelSize })
            ]
          })
        ],
        listeners: {
          // draw colored squares on move
          move: function (event) {
            var context = event.target.getContext('2d')
            // calculate the angle of the drag direction
            var dragAngle = 180 * Math.atan2(event.dx, event.dy) / Math.PI

            // set color based on drag angle and speed
            context.fillStyle =
              'hsl(' +
              dragAngle +
              ', 86%, ' +
              (30 + Math.min(event.speed / 1000, 1) * 50) +
              '%)'

            // draw squares
            context.fillRect(
              event.pageX - pixelSize / 2,
              event.pageY - pixelSize / 2,
              pixelSize,
              pixelSize
            )
          }
        }
      })
      // clear the canvas on doubletap
      .on('doubletap', function (event) {
        var context = event.target.getContext('2d')

        context.clearRect(0, 0, context.canvas.width, context.canvas.height)
        resizeCanvases()
      })

    function resizeCanvases () {
      [].forEach.call(document.querySelectorAll('.rainbow-pixel-canvas'), function (
        canvas
      ) {
        delete canvas.width
        delete canvas.height

        var rect = canvas.getBoundingClientRect()

        canvas.width = rect.width
        canvas.height = rect.height
      })
    }

    resizeCanvases()

    // interact.js can also add DOM event listeners
    interact(window).on('resize', resizeCanvases)
  },
}
</script>

<style scoped>
.rainbow-pixel-canvas {
  width: 100%;
  height: 200px;
  box-sizing: border-box;
  background: white;
  border: 1px solid #ccc;

  webkit-user-select: none;
  user-select: none;
  -ms-touch-action: none;
      touch-action: none;
}
p {
  text-align: center;
  font-family: monospace;
  font-size: 1.25rem;
}
</style>