<template>
  <main>
    <!-- heading -->
    <header>
      <img src="https://pinia.vuejs.org/logo.svg" alt="pinia logo" />
      <h1><span>Pinia T</span><span class="a">a</span>sk</h1>
    </header>
    <!-- filter -->
    <task-form />
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'fav'">Favorites tasks</button>
    </nav>
    <!-- loading -->
    <div class="loading" v-if="isLoading">Loading ....</div>
    <!-- task List -->

    <div class="task-list" v-if="filter === 'all' && !isLoading">
      <p>You have {{ totalCount }} tasks left to do</p>
      <div v-for="task in tasks" :key="task.id">
        <task-details :task="task"></task-details>
      </div>
    </div>
    <div class="task-list" v-if="filter === 'fav' && !isLoading">
      <p>You have {{ favCount }} Favorite tasks</p>
      <div v-for="task in favs" :key="task">
        <task-details :task="task"></task-details>
      </div>
    </div>
    <div class="reset">
      <button @click="taskStore.$reset">RESET STATE</button>
    </div>
  </main>
</template>

<script>
import { ref } from "vue";
import TaskDetails from "./components/TaskDetails.vue";
import { useTaskStore } from "./Store/TaskStore";
import TaskForm from "./components/TaskForm.vue";
import { storeToRefs } from "pinia";
export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const taskStore = useTaskStore();
    const { tasks, isLoading, favs, totalCount, favCount } =
      storeToRefs(taskStore);
    const filter = ref("all");
    taskStore.getTasks();
    return { taskStore, filter, tasks, isLoading, favs, totalCount, favCount };
  },
};
</script>
