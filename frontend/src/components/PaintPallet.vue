<template>
  <div class="comp">
    <div>
        <canvas 
            :width = "canvasWidth"
            :height = "canvasHeight"
            ref="canvas"
            @mousemove = "draw"
            @mousedown = "changeMode"
            @mouseup   = "changeMode"
        ></canvas>
    </div>
    <span id="outputImg">
        <span id="radioSpace">
            <Radio tag=出力形式
                :radioTitle = "radioTitle"
                :radioVal = "imageFormatKey"
                :setVal = "setImageFormat"
                :keys = "keyVals"
                :vals = "radioVals"
                :labels = "radioLabels"
            />
        </span>
        <span id="btnSpace">
            <Button tag = 画像出力ボタン
                :btnLabel = "buttonLabel"
                :pushBtn = "outputPicture"
            /> 
        </span>
    </span>
  </div>
</template>

<script>
import Radio from "./Radio"
import Button from "./Button"
const DEFAULT_IMG_FMT_KEY = "0"
const COMPRESSION_RATIO = 1

export default {
    name: "A_PaintPallet",
    components: {
        Radio,
        Button,
    },
    props: {
        color        : String,
        fontSize     : String,
        canvasWidth  : String,
        canvasHeight : String,
    },
    data: function(){
        return {
            is_drawing_mode: false,

            // Radio -> image format
            radioTitle: "出力形式",
            imageFormatKey: DEFAULT_IMG_FMT_KEY,
            keyVals: ["0", "1"],
            radioVals: ["0", "1"],
            radioLabels: ["png", "jpg"],

            // Button -> to output picture
            buttonLabel: "画像出力",
        }
    },
    mounted: function() {
        this.canvas  = this.$refs.canvas;
        this.context = this.canvas.getContext("2d");
        this.rect    = this.canvas.getBoundingClientRect();
    },
    methods: {
        // PaintPallet itself
        draw(e) {
            switch (this.is_drawing_mode){
                case false:
                    break;
                case true:
                {
                    this.context.fillStyle = this.color;
                    this.context.fillRect(
                        e.clientX - this.rect.left,
                        e.clientY - this.rect.top,
                        Number(this.fontSize),
                        Number(this.fontSize),
                    );
                    break;
                }
                default:
                    break;
            }
        },
        changeMode() {
            this.is_drawing_mode = !this.is_drawing_mode;
        },

        // Radio -> image format
        setImageFormat(val) {
            this.imageFormatKey = String(val);
        },

        // Button -> to output picture
        outputPicture() {
            console.log("this.imageFormatKey :",this.imageFormatKey)
            /**
            * https://note.affi-sapo-sv.com/js-canvas-download.php
            * https://developer.mozilla.org/ja/docs/Web/API/HTMLCanvasElement/toBlob
            * 擬似的にaタグ要素とそのurlを作成し、urlをクリックすることで画像をダウンロードすることにする。
            */
            const mapper = {
                "0": "image/png",
                "1": "image/jpeg",
            }
            const format = mapper[this.imageFormatKey];

            this.canvas.toBlob(function(blob) {
                const a = document.createElement("a");
                a.href = URL.createObjectURL(blob);
                a.download = "download";
                a.click();
            },format,COMPRESSION_RATIO)
        }
    }
}
</script>

<style scoped>
canvas {
    border: solid 1px;
}

#outputImg {
    display: flex;
}

#radioSpace {
    margin: 3px;
}

#btnSpace {
    margin: 3px 3px 3px 12px; 
}
</style>