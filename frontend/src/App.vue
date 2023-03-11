<template>
  <div id="app">
    <p>
      Paint as you feel
    </p>
    <selector
      :defaultVal = "fontSize"
      :selectVal = "setFontSize"
      :optionList = "fontSizeList"
    />
    <paint-pallet
      :color = "fontColor"
      :fontSize  = "fontSize"
      :canvasWidth = "canvasWidth"
      :canvasHeight = "canvasHeight"
    />
  </div>
</template>

<script>
import PaintPallet from './components/PaintPallet'
import Selector from "./components/Selector"
const DEFAULT_FONT_SIZE = "3"
const CANVAS_WIDTH = "600"
const CANVAS_HEIGHT = "600"

export default {
  name: 'App',
  components: { 
    PaintPallet,
    Selector,
  },
  data: function(){
    return {
      // Selector -> fontsize
      fontColor: "#40a174",
      fontSize: DEFAULT_FONT_SIZE,
      fontSizeList: [1,2,3,4,5,6,7,8,9,10],
      canvasWidth: CANVAS_WIDTH,
      canvasHeight: CANVAS_HEIGHT,
    }
  },
  methods: {
    // Selector -> fontsize
    setColor(color) {
      this.color = color;
    },
    setFontSize(size) {
      this.fontSize = String(size);
    },
  }
}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin-top: 20px;
}
</style>
