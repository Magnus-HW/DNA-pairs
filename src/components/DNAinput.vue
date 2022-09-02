<script setup>
defineProps(["modelValue"]);
const emit = defineEmits(["update:modelValue"]);

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
    console.log(event.keyCode);
    emit("update:modelValue", event.target.value);
    return true;
  }
  return event.preventDefault();
};
</script>

<template>
  <form>
    <input
      :value="modelValue"
      type="text"
      name="dna"
      id="dna"
      maxlength="100"
      @keypress="inputValidation($event)"
      @input="$event.target.value = $event.target.value.toUpperCase()"
    />
  </form>
</template>

<style scoped>
</style>
