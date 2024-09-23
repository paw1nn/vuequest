<template>
  <div class="drawing-board">
    <canvas
      ref="canvas"
      :width="width"
      :height="height"
      @mousedown="startDrawing"
      @mouseup="stopDrawing"
      @mousemove="draw"
    />
    <button @click="clearCanvas">Clear</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isDrawing: false,
      width: 500,
      height: 500,
      ctx: null,
      lastX: 0,
      lastY: 0,
    };
  },
  mounted() {
    this.ctx = this.$refs.canvas.getContext('2d');
  },
  methods: {
    startDrawing(event) {
      this.isDrawing = true;
      [this.lastX, this.lastY] = this.getMousePosition(event);
    },
    stopDrawing() {
      this.isDrawing = false;
      this.ctx.beginPath();
    },
    draw(event) {
      if (!this.isDrawing) return;

      const [x, y] = this.getMousePosition(event);
      this.ctx.beginPath();
      this.ctx.moveTo(this.lastX, this.lastY);
      this.ctx.lineTo(x, y);
      this.ctx.stroke();
      [this.lastX, this.lastY] = [x, y];
    },
    getMousePosition(event) {
      const rect = this.$refs.canvas.getBoundingClientRect();
      return [event.clientX - rect.left, event.clientY - rect.top];
    },
    clearCanvas() {
      this.ctx.clearRect(0, 0, this.width, this.height);
    },
  },
};
</script>

<style scoped>
.drawing-board {
  position: relative;
  margin: 20px;
}

canvas {
  border: 1px solid black;
}
</style>
