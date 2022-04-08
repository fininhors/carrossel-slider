<template>
  <div class="carrossel">
    <div class="carrossel-inner">
      <Indicadores
        v-if="indicators"
        :total="props.slides.length"
        :currentSlide="currentSlide"
        @switch="switchSlide($event)"
      />

      <Item
        v-for="(slide, index) in slides"
        :key="`item-${index}`"
        :slide="slide"
        :currentSlide="currentSlide"
        :index="index"
        :direction="direction"
        @mouseenter="stopSlideTimer"
        @mouseout="startSlideTimer"
      />
      <Controles v-if="controls" @prev="prev" @next="next" />
    </div>
  </div>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue';
import Item from './Item.vue';
import Controles from './Controles.vue';
import Indicadores from './Indicadores.vue';

const currentSlide = ref(0);
const slideInterval = ref(null);
const direction = ref('right');

const props = defineProps({
  slides: {
    type: Array,
    required: true
  },
  controls: {
    type: Boolean,
    default: false
  },
  indicators: {
    type: Boolean,
    default: false
  },
  interval: {
    type: Number,
    default: 5000
  }
});

function setCurrentSlide (index) {
  currentSlide.value = index;
}

function prev (step = -1) {
  const index = currentSlide.value > 0 ? currentSlide.value + step : props.slides.length - 1;
  setCurrentSlide(index);
  direction.value = 'left';
  startSlideTimer();
}

function _next (step = 1) {
  const index = currentSlide.value < props.slides.length - 1 ? currentSlide.value + step : 0;
  setCurrentSlide(index);
  direction.value = 'right';
}

function next (step = 1) {
  _next(step);
  startSlideTimer();
}

function startSlideTimer () {
  stopSlideTimer();
  slideInterval.value = setInterval(_next, props.interval);
}

function stopSlideTimer () {
  clearInterval(slideInterval.value);
}

function switchSlide (index) {
  const step = index - currentSlide.value;
  if (step > 0) {
    next(step);
  } else {
    prev(step);
  }
}

onMounted(() => {
  startSlideTimer();
});

onBeforeUnmount(() => {
  stopSlideTimer();
});

</script>

<style scoped>
.carrossel {
  display: flex;
  justify-content: center;
}
.carrossel-inner {
  position: relative;
  width: 900px;
  height: 400px;
  overflow: hidden;
}
</style>
