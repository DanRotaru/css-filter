<template>
  <header>
    <div class="title">CSS Filter</div>
    <div class="subtitle">CSS filter generator to convert from black to target hex color</div>

    <div class="wrapper">
      <div>
        <label for="color" class="label-target">Target Color</label>

        <div class="input">
          <label class="label-color" for="color-choice">
            <input type="color"
                   id="color-choice"
                   v-model="color"
                   @change="$emit('color', $event.target.value)"
            />
          </label>
          <input type="text"
                 id="color"
                 class="target"
                 v-model="color"
                 placeholder="HEX Target Color"
                 @change="$emit('color', $event.target.value)"
          />

          <button class="execute" @click="$emit('execute', color)">Compute Filters</button>
        </div>
      </div>

      <div>
        <p id="lossDetail" v-if="loss">Loss: {{ loss }} <b>{{ lossMsg }}</b></p>
      </div>
    </div>
  </header>
</template>

<script setup>
import {ref} from "vue";
const color = ref('#000000');
defineEmits(['color', 'execute']);
defineProps(['loss', 'lossMsg']);
</script>