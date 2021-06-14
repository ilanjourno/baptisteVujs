<template>
  <form v-on:submit="addColumn($event)">
      <input type="text" :ref="columnTitle" v-on:change="handleChangeTitle"/>
      <button type="submit">Ajouter une colonne</button>
  </form>
  <div class="columns">
    <div
      v-for="(column, index) in columns"
      :key="index"
    >
      <button v-on:click="deleteColumn(index)">Delete</button>
      <Column :title="column.title"/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Column from '@/components/Column.vue';
import { ref } from 'vue';

export default {
  name: 'Home',
  components: {
    Column,
  },
  setup() {
    const columns = ref([]);
    let columnTitle = ref(null);
    const handleChangeTitle = (e) => {
      columnTitle = e.target.value;
    };
    const addColumn = (e) => {
      e.preventDefault();
      const column = {
        title: columnTitle,
      };
      columns.value.push(column);
    };
    const deleteColumn = (index) => {
      columns.value.splice(index, 1);
    };

    return {
      addColumn, columns, columnTitle, handleChangeTitle, deleteColumn,
    };
  },
};
</script>

<style scoped>

  .columns{
    display: flex;
  }

</style>
