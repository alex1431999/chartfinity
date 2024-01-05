<template>
  <div>
    <canvas width="1200" height="1200" ref="canvas"></canvas>
    <canvas width="1200" height="1200" ref="canvasOffScreen"></canvas>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'TradingChart',
  data() {
    return {
      panX: 0,
    };
  },
  computed: {
    canvas(): HTMLCanvasElement {
      return this.$refs.canvas as HTMLCanvasElement;
    },
    canvasOffScreen(): HTMLCanvasElement {
      return this.$refs.canvasOffScreen as HTMLCanvasElement;
    },
    ctx(): CanvasRenderingContext2D {
      return this.canvas.getContext('2d') as CanvasRenderingContext2D;
    },
    canvasOffScreenCtx(): CanvasRenderingContext2D {
      return this.canvasOffScreen.getContext('2d') as CanvasRenderingContext2D;
    },
    lineColor() {
      return '#3498db';
    },
  },
  methods: {
    drawElement() {
      this.canvasOffScreenCtx.clearRect(0, 0, this.canvas.width, this.canvas.height);
      this.canvasOffScreenCtx.beginPath();
      this.canvasOffScreenCtx.moveTo(50 - this.panX, 100);
      this.canvasOffScreenCtx.lineTo(70 - this.panX, 100);
      this.canvasOffScreenCtx.strokeStyle = this.lineColor;
      this.canvasOffScreenCtx.stroke();

      this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);
      this.ctx.drawImage(this.canvasOffScreen, 0, 0);
    },
    panCanvas(direction: 'left' | 'right') {
      if (direction === 'left') {
        this.panX -= 5;
      } else if (direction === 'right') {
        this.panX += 5;
      }

      this.drawElement();
    },
  },
  mounted() {
    this.drawElement();

    (window as any).test = this;
  },
});
</script>
