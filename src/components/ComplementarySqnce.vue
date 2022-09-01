<script setup>
import { ref, watch } from "vue";
import TheTemperature from "./TheTemperature.vue";
import DNAInput from "./DNAInput.vue";
const pairs = {
  A: "T",
  G: "C",
  T: "A",
  C: "G",
};

const dna = ref("");
const complSequence = ref("");
const nucls = ref({
  A: 0,
  G: 0,
  T: 0,
  C: 0,
});

watch(dna, () => {
  nucls.value = {
    A: 0,
    G: 0,
    T: 0,
    C: 0,
  };
  let res = "";

  for (let char of dna.value) {
    res = res.concat(pairs[char]);
    nucls.value[char] += 1;
  }

  complSequence.value = res;
});
</script>

<template>
  <div class="dna-input">
    <DNAInput v-model="dna" />
    <div class="sequence">DNA sequence: {{ dna }}</div>
    <div class="complementary-sequence">
      Complementary DNA sequence: {{ complSequence }}
    </div>
    <TheTemperature :nucls="nucls" :dnaLength="dna.length" />
  </div>
</template>

<style scoped></style>
