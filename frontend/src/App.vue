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
  </div>
</template>

<script>
import PaintPallet from './components/PaintPallet'
import Selector from "./components/Selector"
import Radio from "./components/Radio"
const DEFAULT_FONT_SIZE = "3"
const DEFAULT_IMG_FMT_KEY = "0"

export default {
  name: 'App',
  components: { 
    PaintPallet,
    Selector,
    Radio,
  },
  data: function(){
    return{
      // selector -> fontsize
      fontColor: "#40a174",
      fontSize: DEFAULT_FONT_SIZE,
      fontSizeList: [1,2,3,4,5,6,7,8,9,10],
      
      // radio -> image format
      tag: "画像出力形式",
      radioTitle: "出力形式",
      imageFormatKey: DEFAULT_IMG_FMT_KEY,
      keyVals: ["0", "1", "2"],
      radioVals: ["0", "1", "2"],
      radioLabels: ["png", "jpg", "svg"],
    }
  },
  watch: {
    imageFormatKey: function(val) {
      // TODO //
      console.log("watch val",val);
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
