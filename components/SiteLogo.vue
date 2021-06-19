<template>
    <canvas id="logo--canvas" class="logo--canvas" height="60" width="110" @mouseover="mouseOver">
    </canvas>
</template>

<script>
export default {
    data() {
        return {
            canvas: false, 
            ctx: false, 
            flag: false,
            prevX: 10,
            currX: 10,
            prevY: 57,
            currY: 57,
            dot_flag: false,
            colorLin: "#ff7730",
            colorExp: "#2998ff",
            colorSig: '#55c57a',
            lineWidth: 3,
            isDrawing: true
        }
    },
    methods: {
        async mouseOver() {
            if (this.ctx && this.canvas && !this.isDrawing) {
                this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);
                this.init();
            }
        },
        async init() {
            this.isDrawing = true;
            this.canvas = document.getElementById('logo--canvas');
            this.ctx = this.canvas.getContext("2d");
            await this.drawWSubtractor(this.getSubtractorLin, this.colorLin, .1);
            await this.drawWSubtractor(this.getSubtractorExp, this.colorExp, .1);
            await this.drawWSubtractor(this.getSubtractorSigmoid, this.colorSig, .1);
            this.isDrawing = false;
        },
        async drawWSubtractor(subtractorFunc, color, initSub) {
            var subtractor = initSub;
            this.currX = 10;
            this.currY = 57;
            const initX = 10;
            const initY = 57;
            var y = initY;
            var width = 90;
            for(var x = initX; x < width; x += 3) {
                subtractor = subtractorFunc(x - initX);
                y = initY - subtractor;
                var wait = 0;
                if (x - initX < 30) {
                    wait = 2 * (30 - (x - initX));
                } else if (width - x < 30) {
                    wait = 2 * (30 - (width - x));
                }
                await new Promise(r => setTimeout((localX, localY) => {
                    this.drawNewXY(localX, localY, color);
                    r();
                }, wait, x, y));
            }
        },
        getSubtractorExp(x) {
            return .2 * (x/2.8) ** 1.6;
        },
        getSubtractorLin(x) {
            return x * .2;
        },
        getSubtractorSigmoid(x) {
            var t = x / 8 - 5.825;
            return 50/(1+Math.pow(Math.E, -t));
        },
        async drawNewXY(newX, newY, color) {
            this.prevX = this.currX;
            this.prevY = this.currY;

            this.currX = newX - this.canvas.offsetLeft;
            this.currY = newY - this.canvas.offsetTop;
            this.draw(color)
        },
        draw(color) {
            this.ctx.beginPath();
            this.ctx.moveTo(this.prevX, this.prevY);
            this.ctx.lineTo(this.currX, this.currY);
            this.ctx.strokeStyle = color;
            this.ctx.lineWidth = this.lineWidth;
            this.ctx.stroke();
            this.ctx.closePath();
        }
    },
    mounted: function () {
        this.$nextTick(function () {
            // Code that will run only after the
            // entire view has been rendered
            this.init();
        })
    }
}
</script>

<style lang="scss">
    .logo {
        position: absolute;
    }
</style>