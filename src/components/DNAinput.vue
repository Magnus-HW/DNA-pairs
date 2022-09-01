<script setup>
import { ref, computed } from "vue";
const pairs = {
  A: "T",
  G: "C",
  T: "A",
  C: "G",
};
const dna = ref("");

const complSequence = computed(() => {
  let res = "";
  for (let char of dna.value) {
    res = res.concat(pairs[char]);
  }
  console.log(res);
  return res;
});

function inputValidation(event) {
  // console.log(event.target.selectionStart);
  if (
    event.keyCode == 97 ||
    event.keyCode == 65 ||
    event.keyCode == 84 ||
    event.keyCode == 116 ||
    event.keyCode == 71 ||
    event.keyCode == 103 ||
    event.keyCode == 67 ||
    event.keyCode == 99
  ) {
    console.log(event.keyCode);
    return true;
  }
  //String.fromCharCode(0);
  return event.preventDefault();
}
</script>

<template>
  <div class="dna-input">
    <form>
      <input
        v-model="dna"
        type="text"
        name="dna"
        id="dna"
        @keypress="inputValidation($event)"
        @input="dna = dna.toUpperCase()"
      />
    </form>
    <div>{{ dna }}</div>
    <div class="pairs">{{ complSequence }}</div>
    <div class="temperatuce"></div>
  </div>
</template>

<style scoped></style>
