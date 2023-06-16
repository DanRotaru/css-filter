<template>
  <Header @color="handleInput" @execute="handleExecute" :loss="loss" :lossMsg="lossMsg"/>
  <Main :originalColor="color" :filter="filter"/>
  <Footer/>
</template>

<script setup>
import {ref} from "vue";

import Header from "@/components/Header.vue";
import Main from "@/components/Main.vue";
import Footer from "@/components/Footer.vue";

import {Color, Solver} from './Color'

const color = ref('#000000'),
  loss = ref(null),
  lossMsg = ref(''),
  filter = ref('');

const handleInput = (e) => {
  color.value = e;

  // Auto Execute Handle
  handleExecute();
}

function isValidHexColor(color) {
  // Hex color pattern: starts with '#' followed by 3 or 6 hexadecimal characters
  const hexColorRegex = /^#[0-9A-Fa-f]{3}([0-9A-Fa-f]{3})?$/;
  return hexColorRegex.test(color);
}

const handleExecute = () => {

  if (!isValidHexColor(color.value)) {
    alert('Invalid HEX Color');
    return false;
  }

  const rgbColor = new Color(color.value),
    solver = new Solver(rgbColor),
    result = solver.solve();

  if (result) {
    loss.value = result.loss.toFixed(1);
    filter.value = result.filter;

    if (loss.value < 1) {
      lossMsg.value = 'This is a perfect result.';
    } else if (loss.value < 5) {
      lossMsg.value = 'The is close enough.';
    } else if (loss.value < 15) {
      lossMsg.value = 'The color is somewhat off. Consider running it again.';
    } else {
      lossMsg.value = 'The color is extremely off. Run it again!';
    }
  }
}
</script>