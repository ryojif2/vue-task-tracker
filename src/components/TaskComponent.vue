<template>
  <div>
    <div
      @dblclick="$emit('toggleReminder', taskDetail.id)"
      :class="[taskDetail.reminder ? 'reminder' : '', 'task']"
    >
      <h3>
        {{ taskDetail.text }}
        <i class="fas fa-times" @click="$emit('deleteTask', taskDetail.id)">
        </i>
      </h3>
      <p>{{ taskDetail.day }}</p>
    </div>
  </div>
</template>

<script setup>
// import { toRefs } from "vue";
// import { computed } from "vue";

// eslint-disable-next-line
const props = defineProps(["taskDetail"]);

// const taskDetail = computed(() => props.task);

// const { text, day, id } = toRefs(props.task);
</script>

<style scoped>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
