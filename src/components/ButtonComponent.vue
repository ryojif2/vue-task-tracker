<template>
  <button @click="onClick()" :style="{ background: props.color }" class="btn">
    {{ props.text }}
  </button>
</template>

<script setup>
const props = defineProps(["text", "color"]);
const emit = defineEmits(["btnClick"]);

const onClick = () => {
  emit("btnClick");
};
</script>

<style lang="scss" scoped></style>
