<template>
  <div>
    <AddTask v-if="props.showAddTask" @addTask="addTask" />
    <TasksComponent
      :tasks="tasks"
      @deleteTask="deleteTask"
      @toggleReminder="toggleReminder"
    />
  </div>
</template>

<script setup>
import TasksComponent from "../components/TasksComponent.vue";
import AddTask from "../components/AddTask.vue";
import { ref, onMounted } from "vue";

import axios from "axios";

const props = defineProps(["showAddTask"]);
const tasks = ref([]);

const addTask = async (task) => {
  const res = await axios.post("api/tasks", task);

  tasks.value = [...tasks.value, res.data];
};

const deleteTask = async (id) => {
  if (confirm("Are you sure?")) {
    const res = await axios.delete(`api/tasks/${id}`);

    res.status === 200
      ? (tasks.value = tasks.value.filter((task) => {
          return task.id !== id;
        }))
      : alert("Error deleting task");
  }
};

const toggleReminder = async (id) => {
  const taskToToggle = await fetchTask(id);

  const updateTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

  await axios.put(`api/tasks/${id}`, updateTask);

  tasks.value = tasks.value.map((task) =>
    task.id == id ? { ...task, reminder: !taskToToggle.reminder } : task
  );
};

const fetchTasks = async () => {
  const res = await axios.get("api/tasks");

  return res.data;
};

const fetchTask = async (id) => {
  const res = await axios.get(`api/tasks/${id}`);

  return res.data;
};

// onServerPrefetch(async () => {
//   tasks.value = await fetchTasks();
// });

onMounted(async () => {
  tasks.value = await fetchTasks();
});
</script>

<!-- <script>
import TasksComponent from "../components/TasksComponent.vue";
import AddTask from "../components/AddTask.vue";

import axios from "axios";

export default {
  name: "HomeView",
  components: { TasksComponent, AddTask },
  props: {
    showAddTask: Boolean,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async addTask(task) {
      const res = await axios.post("api/tasks", task);

      this.tasks = [...this.tasks, res.data];
    },
    async deleteTask(id) {
      if (confirm("Are you sure?")) {
        const res = await axios.delete(`api/tasks/${id}`);

        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => {
              return task.id !== id;
            }))
          : alert("Error deleting task");
      }
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id);

      const updateTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

      await axios.put(`api/tasks/${id}`, updateTask);

      this.tasks = this.tasks.map((task) =>
        task.id == id ? { ...task, reminder: !taskToToggle.reminder } : task
      );
    },

    async fetchTasks() {
      const res = await axios.get("api/tasks");

      return res.data;
    },

    async fetchTask(id) {
      const res = await axios.get(`api/tasks/${id}`);

      return res.data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script> -->
