<template>
  <div id="app">
    <p>
      Paint as you feel
    </p>
    <selector
      :defaultVal = "fontSize"
      :selectEl = "setFontSize"
      :optionList = "fontSizeList"
    />
    <paint-pallet
      :color = "fontColor"
      :fontSize  = "fontSize"
    />
    <Radio tag=出力形式
      :radioTitle = "radioTitle"
      :defaultVal = "defaultRadioVal"
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

export default {
  name: 'App',
  components: { 
    PaintPallet,
    Selector,
    Radio,
  },
  data: function(){
    return{
      fontColor: "#40a174",
      fontSize: DEFAULT_FONT_SIZE,
      fontSizeList: [1,2,3,4,5,6,7,8,9,10],
      
      // radio
      currentRadioVal: "0",

      tag: "画像出力形式",
      radioTitle: "出力形式",
      defaultRadioVal: "0",
      radioVals: ["0", "1", "2"],
      radioLabels: ["png", "jpg", "svg"],
    }
  },
  watch: {
    currentRadioVal: function(val) {
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
  }
}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin-top: 20px;
}
</style>
