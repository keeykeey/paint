<template>
  <div>
    <button ref="presentColor" class="presentColor"></button>
    <canvas
      ref="canvas"
      :width="width"
      :height="height"
      @click="chooseFontColor"
    />
    <input class="bar" type="range" min="0" max="255" step="1" v-model="rc"/>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        rc: null,
        gc: null,
        bc: null,
        canvas: null,
        context: null,
        rect: null,
        presentColorCode: "",
        colorButton: null,
      }
    },
    props: {
      defaultColor: String,
      propColor: Function,
      width: Number,
      height: Number,
    },
    mounted() {
      this.rc = this.defaultColor.substring(1,3);
      this.canvas = this.$refs.canvas;
      this.context = this.canvas.getContext("2d");
      this.mapColors(this.context);

      this.rect = this.canvas.getBoundingClientRect();

      this.colorButton = this.$refs.presentColor;
      this.colorButton.style.backgroundColor = this.defaultColor
    },
    watch: {
      rc() {
        this.mapColors(this.context);
      },
      presentColorCode(code) {
        this.propColor(code);
        this.colorButton.style.backgroundColor = code;
      }
    },
    methods: {
      _10to16AsString(val) {
        let ret = Number(val).toString(16);
        if (ret.length == 0) {
          return "00";
        } else if (ret.length == 1) {
          return "0" + ret;
        } else {
          return ret;
        }
      },
      mapColors(context) {
        for (let g=0; g<=255; g++) {
          for (let b=0; b<=255; b++) {
            const r0x = this._10to16AsString(this.rc);
            const g0x = this._10to16AsString(g);
            const b0x = this._10to16AsString(b);
            const colorCode = `#${r0x}${g0x}${b0x}`;
            context.fillStyle = colorCode;
            context.fillRect(g, b, this.height/256, this.width/256)
          }
        }
      },
      chooseFontColor(e) {
        const gN = Number(e.clientX) - Number(this.rect.left);
        const bN = Number(e.clientY) - Number(this.rect.top);
        const r0x = this._10to16AsString(this.rc);
        const g0x = this._10to16AsString(gN);
        const b0x = this._10to16AsString(bN);
        const colorCode = `#${r0x}${g0x}${b0x}`;
        this.presentColorCode = colorCode;
      },
      toggleStyle() {
        /** TODO */
        this.canvas.classList.toggle("is-hidden");
      }
    },
  }
</script>

<style scoped>
  .presentColor {
    position: absolute;
    top: 72px;
    left: 657px;
    width: 50px;
    height: 18px;
    border: solid 1px;
  }
  canvas {
    position: absolute;
    top: 90px;
    left: 620px;
    border: solid 1px;
    transition:
      border-top .3s ease-out;
  }
  canvas.is-hidden {
    opacity: 0;
  }
  .bar {
    position: absolute;
    top: 350px;
    left: 618px;
    width: 256px;
  }
</style>