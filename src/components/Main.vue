<template>
  <main>
    <div class="color">
      <p>Real pixel, color applied through CSS background-color:</p>
      <div class="pixel" id="realPixel" :style="'background-color: ' + originalColor"></div>
    </div>
    <div class="color">
      <p>Filtered pixel, color applied through CSS filter:</p>
      <div class="pixel" id="filterPixel" :style="filter"></div>
    </div>
  </main>

  <code id="result" v-if="filter" v-html="formatString(filter)"></code>
</template>

<script setup>
defineProps(['originalColor', 'filter']);

const formatString = (str) => str.replace(/(\d+[%deg]+)/g, "<n>$&</n>").replace(/^(\s*filter:\s*)/, "<k>$1</k>");
</script>