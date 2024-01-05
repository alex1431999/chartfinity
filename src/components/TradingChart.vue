<template>
  <canvas width="1200" height="1200" ref="canvas"></canvas>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'TradingChart',
  computed: {
    canvas(): HTMLCanvasElement {
      return this.$refs.canvas as HTMLCanvasElement;
    },
    ctx(): CanvasRenderingContext2D {
      const context = this.canvas.getContext('2d');

      if (!context) {
        throw Error('The canvas was not rendered');
      }

      return context;
    },
    lineColor() {
      return '#3498db';
    },
  },
  mounted() {
    this.ctx.moveTo(0, 0);
    this.ctx.lineTo(200, 200);
    this.ctx.strokeStyle = this.lineColor;
    this.ctx.stroke();
  },
});
</script>
