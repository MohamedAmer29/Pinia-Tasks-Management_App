<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <input
        type="text"
        placeholder="I need to ..."
        v-model="newTask"
        class="input"
      />
      <button class="add">Add</button>
    </form>
  </div>
</template>

<script>
import { useTaskStore } from "@/Store/TaskStore";
import { ref } from "vue";
export default {
  setup() {
    const taskStore = useTaskStore();
    const newTask = ref("");

    const handleSubmit = () => {
      if (newTask.value.length > 0) {
        let id = taskStore.tasks[taskStore.tasks.length - 1].id + 1;
        taskStore.addTask({
          title: newTask.value,
          isFav: false,
          id: toString(id),
        });
        newTask.value = "";
      }
    };
    return { newTask, handleSubmit };
  },
};
</script>
<style scoped>
form {
  margin-bottom: 30px;
  height: 40px;
  max-width: 560px;
  margin: auto;
  display: flex;
  text-align: center;

  padding-top: 40px;
  padding-bottom: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}
div {
  background: #e7e7e7;
}
.input {
  border-color: rgb(175, 171, 171);
  background-color: #ffe464;
  padding: 8px;
  border-radius: 8px;

  width: 50%;
  margin: 15px;
  font-size: 1.2rem;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  color: #54ac60;
}
.input::placeholder {
  color: #54ac60;
}
.input:focus {
  box-shadow: 0 0 10px rgb(117, 116, 116);
}

.add {
  background-color: #54ac60;
  padding: 3px;
  width: 3.5rem;
  font-size: 1.2rem;
  border-radius: 8px;
  border: none;
  cursor: pointer;
  color: #ffe464;
}
.add:hover {
  opacity: 80%;
}
.add:active {
  box-shadow: 0 2px 4px black;
}
</style>
