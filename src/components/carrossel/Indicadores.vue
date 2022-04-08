<template>
  <div class="carrossel-indicadores">
    <div
      v-for="(item, index) in total"
      :key="index"
      class="carrossel-indicador-item"
      :class="{ active: currentSlide === index }"
      @click="switchSlide(index)"
    ></div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  total: {
    type: Number,
    required: true
  },
  currentSlide: {
    type: Number,
    required: true
  }
});

const emit = defineEmits(['switchSlide']);

function switchSlide (index) {
  emit('switch', index);
}
</script>

<style scoped>
.carrossel-indicadores {
  bottom: 1.5em;
  display: flex;
  left: 50%;
  position: absolute;
  transform: translateX(-50%);
  z-index: 2;
}
.carrossel-indicador-item {
  background-color: #fff;
  border: none;
  border-radius: 50%;
  cursor: pointer;
  height: 20px;
  margin: 0.2em;
  opacity: 0.5;
  width: 20px;
}
.active {
  opacity: 1;
}
</style>
