<template>
  <div id="app">
    <p>
      Paint as you feel
    </p>
    <div id="fontSelector">
      <selector
        :defaultVal = "fontSize"
        :selectVal = "setFontSize"
        :optionList = "fontSizeList"
      />
    </div>
    <choose-font-color
      :defaultColor = "fontColor"
      :propColor = "propColor"
      :width = "Number(256)"
      :height = "Number(256)"
    ></choose-font-color>
    <paint-pallet
      :color = "fontColor"
      :fontSize  = "fontSize"
      :canvasWidth = "canvasWidth"
      :canvasHeight = "canvasHeight"
    />
  </div>
</template>

<script>
import PaintPallet from "./components/PaintPallet"
import ChooseFontColor from "./components/ChooseFontColor"
import Selector from "./components/Selector"
const DEFAULT_FONT_COLOR = "#000000"
const DEFAULT_FONT_SIZE = "3"
const CANVAS_WIDTH = "600"
const CANVAS_HEIGHT = "500"

export default {
  name: 'App',
  components: { 
    PaintPallet,
    ChooseFontColor,
    Selector,
  },
  data: function(){
    return {
      // Selector -> fontsize
      fontColor: DEFAULT_FONT_COLOR,
      fontSize: DEFAULT_FONT_SIZE,
      fontSizeList: [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20],
      canvasWidth: CANVAS_WIDTH,
      canvasHeight: CANVAS_HEIGHT,
    }
  },
  methods: {
    // Selector -> SelectFontColor
    propColor(color) {
      this.fontColor = String(color);
    },
    // Selector -> fontsize
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
#fontSelector {
  position: absolute;
  top: 70px;
  left: 620px;
}
</style>
