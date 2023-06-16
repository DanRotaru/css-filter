<template>
  <footer>
    <div style="display: none">
      &copy; {{ year }}
    </div>
  </footer>
</template>

<script setup>
const year = new Date().getFullYear();
</script>