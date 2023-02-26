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
    />
    <Radio tag=出力形式
      :radioTitle = "radioTitle"
      :radioVal = "imageFormatKey"
      :setVal = "setImageFormat"
      :keys = "keyVals"
      :vals = "radioVals"
      :labels = "radioLabels"
    ></Radio>
    <Button tag = 画像出力ボタン
      :btnLabel = "buttonLabel"
      :pushBtn = "outputPicture"
    >
    </Button>
  </div>
</template>

<script>
import PaintPallet from './components/PaintPallet'
import Selector from "./components/Selector"
import Radio from "./components/Radio"
import Button from "./components/Button"
const DEFAULT_FONT_SIZE = "3"
const DEFAULT_IMG_FMT_KEY = "0"

export default {
  name: 'App',
  components: { 
    PaintPallet,
    Selector,
    Radio,
    Button,
  },
  data: function(){
    return {
      // Selector -> fontsize
      fontColor: "#40a174",
      fontSize: DEFAULT_FONT_SIZE,
      fontSizeList: [1,2,3,4,5,6,7,8,9,10],
      
      // Radio -> image format
      radioTitle: "出力形式",
      imageFormatKey: DEFAULT_IMG_FMT_KEY,
      keyVals: ["0", "1", "2"],
      radioVals: ["0", "1", "2"],
      radioLabels: ["png", "jpg", "svg"],

      // Button -> to output picture
      buttonLabel: "画像出力",
    }
  },
  methods: {
    setColor(color) {
      this.color = color;
    },
    setFontSize(size) {
      this.fontSize = String(size);
    },
    setImageFormat(val) {
      this.imageFormatKey = String(val);
    },
    outputPicture(){
      console.log("output picture in format type : ",this.imageFormatKey);
      /**
       * TODO
       * https://note.affi-sapo-sv.com/js-canvas-download.php
       */
    }
  }
}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin-top: 20px;
}
</style>
