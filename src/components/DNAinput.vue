<script setup>
import { ref } from "vue";

defineProps(["modelValue"]);
const emit = defineEmits(["update:modelValue"]);

const maxLengthFlag = ref(false);

function inputValidation(event) {
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
    return true;
  }
  return event.preventDefault();
}

function handleInput(event) {
  if (event.target.value.length == 100) {
    maxLengthFlag.value = true;
  } else {
    maxLengthFlag.value = false;
  }
  const input = event.target;
  const start = input.selectionStart;
  const end = input.selectionEnd;
  input.value = input.value.toLocaleUpperCase();
  input.setSelectionRange(start, end);

  emit("update:modelValue", event.target.value);
}
</script>

<template>
  <form>
    <label for="dna" id="dna-label">Enter DNA sequence</label>
    <input
      :value="modelValue"
      type="text"
      name="dna"
      id="dna"
      autocomplete="off"
      maxlength="100"
      :class="{ reachedMaxLength: maxLengthFlag }"
      @keypress="inputValidation($event)"
      @input="handleInput($event)"
      autocapitalize="characters"
    />
  </form>
</template>

<style scoped>
input {
  display: block;
  padding: 3px;
  margin: 3px 0 10px;
}
input:focus {
  /* border: 1px solid black; */
  outline: none;
  background-color: #ebe9e5;
  text-transform: uppercase;
}
input.reachedMaxLength {
  border: 2px solid red;
}
</style>
