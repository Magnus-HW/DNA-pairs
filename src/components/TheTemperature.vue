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
  return props.dnaLength < 13
    ? tempDnalengthLess13(props.nucls)
    : tempDnalengthMore13(props.nucls);
});

function tempDnalengthLess13(nucls) {
  return (2 * (nucls.A + nucls.T) + 4 * (nucls.G + nucls.C)).toFixed(3);
}

function tempDnalengthMore13(nucls) {
  return (
    64.9 +
    (41 * (nucls.G + nucls.C - 16.4)) / (nucls.A + nucls.T + nucls.G + nucls.C)
  ).toFixed(3);
}
</script>

<template>
  <div class="temperature">Melting Temperature: {{ temperature }}</div>
</template>

<style scoped></style>
