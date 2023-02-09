<template>
  <div>
    <div v-for="task in tasks" :key="task.id">
      <TaskComponent
        :taskDetail="task"
        @deleteTask="$emit('deleteTask', task.id)"
        @toggleReminder="$emit('toggleReminder', task.id)"
      />
    </div>
  </div>
</template>

<script setup>
import TaskComponent from "./TaskComponent.vue";

defineProps(["tasks"]);
</script>

<style scoped></style>
