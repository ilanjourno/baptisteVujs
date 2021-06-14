<template>
  <div class="task mx-2">
      <h1>Nom : {{name}}</h1>
      <h3>Description : {{description}}</h3>
      <h5>Date due : {{date}}</h5>
  </div>
</template>

<script>
export default {
  name: 'Task',
  props: {
    name: String,
    description: String,
    date: Date,
  },
};
</script>

<style scoped>
.task {
  background-color: white;
  min-height: 100px;
  color: black;
}
</style>
