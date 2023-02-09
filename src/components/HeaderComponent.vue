<template>
  <header>
    <h1>{{ props.title }}</h1>
    <ButtonComponent
      :text="props.showAddTask ? 'Close' : 'Add Task'"
      :color="props.showAddTask ? 'red' : 'green'"
      @btnClick="$emit('toggleAdd')"
    />
  </header>
</template>

<script setup>
import ButtonComponent from "./ButtonComponent.vue";

const props = defineProps({
  title: String,
  showAddTask: Boolean,
});
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
