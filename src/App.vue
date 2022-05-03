<script setup lang="ts">
import { ref, onMounted, computed } from "vue"
const el = ref<HTMLCanvasElement>()

const WIDTH = 600
const HEIGHT = 600

function init() {
  line(WIDTH / 2, HEIGHT, WIDTH / 2, HEIGHT / 2)
}


function line(x1: number, y1: number, x2: number, y2: number) {
  const ctx = el.value?.getContext("2d")!
  ctx.beginPath();
  ctx.strokeStyle = '#000'
  ctx.moveTo(x1, y1);
  ctx.lineTo(x2, y2);
  ctx.stroke();
}

onMounted(() => {
  init()
})


</script>

<template>
  <canvas ref="el" id="canvas"></canvas>
</template>


<style>
#canvas {
  width: 600px;
  height: 600px;
  border: 1px solid #ccc;
}
</style>
