<template>
  <div class="App" ref="appRef">
    <canvas ref="elCanvas" style="border: 1px dashed green"></canvas>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';

//Consider the screen as a canvas with dimensions 600x600.
const CANVAS_DIM = 600;

const appRef = ref();
const circles = ref();
const elCanvas = ref();

const getCircles = async () => {
  const response = await fetch('https://puelle.me/api/comments', {
    headers: {
      'Content-Type': 'application/json',
      Accept: 'application/json',
    },
  });

  const data = await response.json();

  return data.data;
};

const drawCircle = (color, id, position) => {
  const x = (position[0] * elCanvas.value.width) / CANVAS_DIM;
  const y = (position[1] * elCanvas.value.height) / CANVAS_DIM;

  const context = elCanvas.value.getContext('2d');

  context.beginPath();
  context.arc(x, y, 32, 0, Math.PI * 2);
  context.strokeStyle = color;

  context.fillStyle = 'rgba(0, 0, 0, 0)';
  context.lineWidth = 2;
  context.stroke();
  context.fill();

  context.textAlign = 'center';
  context.textBaseline = 'middle';
  context.fillStyle = color;
  context.fillText(id, x, y);
};

onMounted(async () => {
  circles.value = await getCircles();

  const { right, bottom } = appRef.value.getBoundingClientRect();
  elCanvas.value.height = bottom;
  elCanvas.value.width = right;

  circles.value.forEach(({ color, id, position }) => {
    drawCircle(color, id, position);
  });
});
</script>

<style>
.App {
  padding: 0;
  margin: 0;
  font-family: sans-serif;
  text-align: center;
  position: relative;

  width: 100vw;
  height: 100vh;
}
</style>
