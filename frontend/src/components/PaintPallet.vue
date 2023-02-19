<template>
  <div class="comp">
    <div>
        <canvas 
            width = "600"
            height = "600"
            class="canvas" ref="canvas"
            @mousemove = "draw"
            @mousedown = "changeMode"
            @mouseup   = "changeMode"
         ></canvas>
    </div>
  </div>
</template>

<script>
export default {
    name: "A_PaintPallet",
    props: {
        color     : String,
        fontSize  : String,
    },
    data: function(){
        return {
            is_drawing_mode: false,
        }
    },
    mounted: function(){
        this.canvas  = this.$refs.canvas;
        this.context = this.canvas.getContext("2d");
        this.rect    = this.canvas.getBoundingClientRect();
    },
    methods: {
        draw(e){
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
        changeMode(){
            this.is_drawing_mode = !this.is_drawing_mode;
        }
    }
}


</script>



<style scoped>
canvas{
    border:solid 1px;
}
</style>