<template> 
  <div>
    <div class="toolBar">
      <button @click="deleteElement" v-if="showDelete == true">X</button>
      <button @click="this.blocks.push({'id':this.blocks.length})">+</button>
    </div>
    <div id="canvas" style="position: relative;">
      <vue-draggable-resizable id="luckysheet" class="element" @showDelete="updateparent" :w="400" :h="400" :parent="false" :handles="['tr','tl','br','bl']"/>
      <vue-draggable-resizable class="element" @showDelete="updateparent" :w="400" :h="400" :parent="false" :id="i.id" :idElement="i.id" :handles="['tr','tl','br','bl']" v-for="i in blocks" :key="i.id"/>
    </div>
  </div>
  <HelloWorld/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import VueDraggableResizable from './vendor/vue-draggable-resizable'
import './vendor/vue-draggable-resizable.css'
import './themes/main.css'

export default {
  name: 'app',
  components: {
    VueDraggableResizable,
    HelloWorld
  },
  data() {
    return {
      blocks: [
        {'id':0,},
        {'id':1,},
      ],
      showDelete: false,
    }
  },
  mounted() {
    localStorage.selected = -1

    window.addEventListener('resize', this.handleResize);
    this.handleResize();

    this.blocks = [{'id':0,}]

    
  },
  unmounted() {
    window.removeEventListener('resize', this.handleResize);
  },
  methods: {
    handleResize() {
      document.getElementById('canvas').style.width = (window.innerWidth-20)+'px';
      document.getElementById('canvas').style.height = (window.innerHeight-20)+'px';
    },
    updateparent(variable) {
      setTimeout(this.showDelete = variable, 800);
    },
    deleteElement() {
      this.blocks.splice(localStorage.selected,1)
    }
  },
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
