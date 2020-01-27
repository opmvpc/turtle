<template>
  <div id="app" class="h-screen flex flex-col">
    <nav class="w-full flex justify-between items-center bg-purple-600 py-4 border-solid border-b-8 border-purple-700 px-5">
      <div class="branding">
        <span class="text-3xl">🐢</span>
        <span class="text-xl text-yellow-400 font-bold">Turtle graphics editor</span>
      </div>
    </nav>

    <div class="flex w-full h-full">
      <div class="flex flex-col w-1/2 h-full">
        <h1 class="text-center text-xl text-purple-600 font-bold py-5">Code editor</h1>
        <MonacoEditor
          theme="vs"
          language="javascript"
          :options="options"
          @change="onChange"
        ></MonacoEditor>
      </div>
      <div class="flex flex-col w-1/2 h-full">
        <h1 class="text-center text-xl text-purple-600 font-bold py-5">Canvas</h1>
        <vue-p5
          class="flex justify-center"
          @draw="draw"
          @setup="setup">
        </vue-p5>
      </div>
    </div>
  </div>
</template>

<script>
import MonacoEditor from 'monaco-editor-vue';
import VueP5 from 'vue-p5';

export default {
  name: "App",
  components: {
    MonacoEditor,
    "vue-p5": VueP5
  },
  data() {
    return {
      sketch: null,
      options: {
        //Monaco Editor Options
      }
    }
  },
  methods: {
    onChange(value) {
      console.log(value);
      this.draw(this.sketch, value)
    },
    setup(sketch) {
      sketch.createCanvas(400, 400);
      this.sketch = sketch
    },
    draw(sketch, code) {
      eval(code)
    }
  }
}
</script>

<style src="./assets/css/index.css">
