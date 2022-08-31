<script setup>
import { ref } from "vue";
const dna = ref("");
function inputValidation(event) {
  // console.log(event.target.selectionStart);
  // console.log(event.keyCode);
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
    return String.fromCharCode(0);
  }
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
        style="text-transform: uppercase"
        @keypress="inputValidation($event)"
      />
    </form>
    <div>{{ dna }}</div>
    <div class="pairs"></div>
    <div class="temperatuce"></div>
  </div>
</template>

<style scoped></style>
