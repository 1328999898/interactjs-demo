<template>
  <BaseDemo></BaseDemo>
  <DraggableDemo></DraggableDemo>
  <ResizingDemo></ResizingDemo>
  <TransfromDemo></TransfromDemo>
  <CanvasDemo></CanvasDemo>
</template>

<script>
import BaseDemo from './components/BaseDemo.vue'
import DraggableDemo from './components/DraggableDemo.vue'
import ResizingDemo from './components/ResizingDemo.vue'
import TransfromDemo from './components/TransfromDemo.vue'
import CanvasDemo from './components/CanvasDemo.vue'
export default {
  name: 'App',
  components: {
    BaseDemo,
    DraggableDemo,
    ResizingDemo,
    TransfromDemo,
    CanvasDemo,
  }
}
</script>
