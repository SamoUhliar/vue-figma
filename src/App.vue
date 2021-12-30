<template>
  <div>
    <div id="canvas" style="border: 1px solid red; position: relative;">
      <vue-draggable-resizable :w="400" :h="400" :parent="true" v-for="i in blocks" :key="i"/>
    </div>
  </div>
</template>

<script>
import VueDraggableResizable from './vendor/vue-draggable-resizable'
import './vendor/vue-draggable-resizable.css'

export default {
  name: 'app',
  components: {
    VueDraggableResizable
  },
  data() {
    return {
      blocks: 0,
    }
  },
  mounted() {
    window.addEventListener('resize', this.handleResize);
    this.handleResize();
    this.blocks = 1
  },
  unmounted() {
    window.removeEventListener('resize', this.handleResize);
  },
  methods: {
    handleResize() {
      document.getElementById('canvas').style.width = (window.innerWidth-20)+'px';
      document.getElementById('canvas').style.height = (window.innerHeight-20)+'px';
      console.log('d')
    }
  }
}
</script>

<style>
  .vdr {
    border: 1px dashed black;
  }
  #canvas {
    margin: auto;
  }
</style>
