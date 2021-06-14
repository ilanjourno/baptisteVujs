<template>
  <div class="column mx-2 bg-primary text-white">
      <h1>{{title}}</h1>
      <form v-on:submit="addTask">
        <label for="taskName">Nom :</label>
        <input type="text" id="taskName" :ref="taskName" v-on:change="handleChangeTaskname"/>
        <br/>
        <label for="taskDescription">Description :</label>
        <input type="text" id="taskDescription"
        :ref="taskDescription" v-on:change="handleChangeTaskDescription"/>
        <br/>
        <label for="taskDate">Date due :</label>
        <input type="date" id="taskDate" :ref="taskDate" v-on:change="handleChangeTaskDate"/>
        <br/>
        <button type="submit">Ajouter la tâche</button>
      </form>
      <br/>
      <div class="tasks">
        <div
          v-for="(task, index) in tasks"
          :key="index"
        >
          <button v-on:click="deleteTask(index)">Delete Task</button>
          <Task :name="task.name" :description="task.description" :date="task.date"/>
        </div>
      </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import Task from './Task.vue';

export default {
  name: 'Column',
  components: {
    Task,
  },
  props: {
    title: String,
  },
  setup() {
    let taskName = ref(null);
    let taskDescription = ref(null);
    let taskDate = ref(null);
    const tasks = ref([]);

    const addTask = (e) => {
      e.preventDefault();
      const task = {
        name: taskName,
        description: taskDescription,
        date: taskDate,
      };
      tasks.value.push(task);
    };
    const handleChangeTaskname = (e) => {
      taskName = e.target.value;
    };
    const handleChangeTaskDescription = (e) => {
      taskDescription = e.target.value;
    };
    const handleChangeTaskDate = (e) => {
      taskDate = e.target.value;
    };
    const deleteTask = (index) => {
      tasks.value.splice(index, 1);
    };

    return {
      taskName,
      taskDescription,
      taskDate,
      tasks,
      addTask,
      deleteTask,
      handleChangeTaskname,
      handleChangeTaskDescription,
      handleChangeTaskDate,
    };
  },
};
</script>

<style scoped>
.column {
  max-width: 50%;
  min-width: 25vw;
  height: 100vh;
}
</style>
