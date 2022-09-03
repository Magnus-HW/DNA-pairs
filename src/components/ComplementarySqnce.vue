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
    <div class="sequence">
      <div v-for="(letter, index) in dna" :key="index" class="pair">
        <div class="dna-nucl">{{ dna[index] }}</div>
        <div class="comp-dna-nucl">{{ complSequence[index] }}</div>
      </div>
    </div>
    <TheTemperature :nucls="nucls" :dnaLength="dna.length" />
  </div>
</template>

<style scoped>
.pair {
  display: inline-block;
}
.dna-nucl {
  font-weight: bold;
  color: blue;
  margin: 0 0.4rem 0.5rem 0;
}
.comp-dna-nucl {
  font-weight: bold;
  color: rgb(0, 163, 0);
}
.dna-nucl::after {
  content: "";
  background-color: gray;
  width: 3px;
  height: 10px;
  position: absolute;
  left: 35%;
  top: 95%;
}
</style>
