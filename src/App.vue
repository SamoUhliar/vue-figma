<template>
  <div>
    <div class="toolBar">
      <button @click="this.blocks.push({'id':this.blocks.length})">+</button>
    </div>
    <div id="canvas" style="position: relative;">
      <vue-draggable-resizable :w="400" :h="400" :parent="false" :id="i.id" v-for="i in blocks" :key="i.id"/>
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
      blocks: [{'id':0,}],
    }
  },
  mounted() {
    window.addEventListener('resize', this.handleResize);
    this.handleResize();
    this.blocks = [{'id':0,}]
    console.log(this.blocks)
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
  body {
    background-color: #f2f2f2 !important;
  } 
  .vdr {
    border: 1px dashed black;
  }
  #canvas {
    margin: auto;
  }
  .toolBar{
    position: absolute;
    right: 0px;
    top: 0px;
    z-index: 100;
  }
  .toolBar button{
    margin: 20px;
    padding: 15px;
    font-size: 15px;
    border: 1px solid black;
  }
</style>
