<template>
  <div class="task">
    <h3>{{ task.title }}</h3>
    <div class="icons">
      <i class="material-icons delete" @click="taskStore.delteTask(task.id)"
        >delete</i
      >
      <i
        class="material-icons favorite"
        :class="task.isFav ? 'fav' : ''"
        @click="taskStore.toggleFav(task.id)"
        >favorite</i
      >
    </div>
  </div>
</template>

<script>
import { useTaskStore } from "@/Store/TaskStore";

export default {
  props: ["task"],
  setup() {
    const taskStore = useTaskStore();

    return { taskStore };
  },
};
</script>
<style scoped>
.fav {
  color: red;
}
.delete:hover {
  color: rgb(10, 10, 10);
}
.favorite:hover {
  color: rgb(180, 13, 13);
}
</style>
