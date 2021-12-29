<template>
  <div id="app">
    <div style="height: 500px; width: 500px; border: 1px solid red; position: relative;">
      <vue-draggable-resizable :w="400" :h="400" :parent="true" v-for="i in blocks" :key="i"/>
    </div>
    <button @click="blocks++"></button>
  </div>
</template>

<script>
import VueDraggableResizable from './components/vue-draggable-resizable'
import './components/vue-draggable-resizable.css'

export default {
  name: 'app',
  components: {
    VueDraggableResizable
  },
  data() {
    return {
      blocks: 1
    }
  }
}
</script>

<style>
  .vdr {
    border: 1px dashed black;
  }
</style>
