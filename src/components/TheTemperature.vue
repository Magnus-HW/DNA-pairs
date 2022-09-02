<script setup>
import { computed } from "vue";
const props = defineProps({
  nucls: {
    A: {
      type: Number,
      required: true,
    },
    G: {
      type: Number,
      required: true,
    },
    T: {
      type: Number,
      required: true,
    },
    C: {
      type: Number,
      required: true,
    },
  },
  dnaLength: {
    type: Number,
    required: true,
  },
});

const temperature = computed(() => {
  return props.dnaLength <= 13
    ? tempDnalengthLess13(
        props.nucls.A,
        props.nucls.T,
        props.nucls.G,
        props.nucls.C
      )
    : tempDnalengthMore13(
        props.nucls.A,
        props.nucls.T,
        props.nucls.G,
        props.nucls.C
      );
});

function tempDnalengthLess13(A, G, T, C) {
  return (2 * (A + T) + 4 * (G + C)).toFixed(3);
}

function tempDnalengthMore13(A, G, T, C) {
  return (64.9 + (41 * (G + C - 16.4)) / (A + T + G + C)).toFixed(3);
}
</script>

<template>
  <div class="temperature">Melting Temperature: {{ temperature }}</div>
</template>

<style scoped></style>
