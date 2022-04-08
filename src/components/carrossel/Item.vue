<template>
  <transition :name="transitionEffect">
    <div
      class="carrossel-item"
      v-show="currentSlide === index"
      @mouseenter="mouseenter"
      @mouseout="mouseout"
    >
      <img :src="slide" />
    </div>
  </transition>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  slide: {
    type: String,
    required: true
  },
  currentSlide: {
    type: Number,
    required: true
  },
  index: {
    type: Number,
    required: true
  },
  direction: {
    type: String
  }
});

const emit = defineEmits(['mouseenter', 'mouseout']);

function mouseenter () {
  emit('mouseenter');
}
function mouseout () {
  emit('mouseout');
}

const transitionEffect = computed(() => {
  return (props.direction === 'right') ? 'slide-out' : 'slide-in';
});

</script>

<style scoped>
.carrossel-item {
  position: absolute;
  inset: 0;
}
.slide-in-enter-active,
.slide-in-leave-active,
.slide-out-enter-active,
.slide-out-leave-active {
  transition: all 1s ease-in-out;
}
.slide-in-enter-from {
  transform: translateX(-100%);
}
.slide-in-leave-to {
  transform: translateX(100%);
}
.slide-out-enter-from {
  transform: translateX(100%);
}
.slide-out-leave-to {
  transform: translateX(-100%);
}
</style>
