<template> 
  <div>
    <div class="toolBar">
      <button @click="deleteElement" v-if="showDelete == true">X</button>
      <button @click="addBlock('<ion-button>👋</ion-button>')">html</button>
      <button @click="addBlock('Ahoj Psycho 👋')">text</button>
      <button @click="addBlock('<lucky-sheet><lucky-sheet/>')">LuckySheet</button>
      <button @click="addBlock('<code-js></code-js>')">JS</button>
    </div>
    <div id="canvas" style="position: relative;">
      <my-draggable-resizable class="element" @showDelete="updateparent" :w="400" :h="400" :parent="false" :htmlInput="i.type" :id="i.id" :idElement="i.id" :handles="['tr','tl','br','bl']" v-for="i in blocks" :key="i.id"/>
      <vue-draggable-resizable :w="800" :h="500" :parent="false">
        <HelloWorld :idd='1'/>
      </vue-draggable-resizable>
      <!-- <vue-draggable-resizable :w="800" :h="500" :parent="false">
        <HelloWorld :idd='2'/>
      </vue-draggable-resizable> -->
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

import MyDraggableResizable from './vendor/my-draggable-resizable'
import VueDraggableResizable from './vendor/vue-draggable-resizable'
import './vendor/my-draggable-resizable.css'
import './vendor/vue-draggable-resizable.css'
import './themes/main.css'

export default {
  name: 'app',
  components: {
    MyDraggableResizable,
    VueDraggableResizable,
    HelloWorld
  },
  data() {
    return {
      blocks: [],
      showDelete: false,
      nextId: 0,
    }
  },
  mounted() {
    localStorage.selected = -1
    window.addEventListener('resize', this.handleResize);
    this.handleResize();
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
    },
    addBlock(typeText){
      this.nextId ++
      this.blocks.push({'id':this.blocks.length,'type':typeText})
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
