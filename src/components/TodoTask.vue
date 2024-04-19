<!-- src/components/TodoTask.vue -->
<template>
    <tr>
      <td>
        <u v-if="task.completed">{{ task.title }}</u>
        <span v-else>{{ task.title }}</span>
      </td>
      <td>
        <input type="checkbox" v-model="task.completed">
      </td>
      <td>
        <button @click="emitDeleteTask">Supprimer</button>
      </td>
    </tr>
  </template>
  

  <style scoped>
tr {
  transition: background-color 0.3s ease;
}

td {
  padding: 8px;
  border-bottom: 1px solid #eee;
}

u {
  text-decoration: line-through;
  color: #bbb;
}

span {
  color: #333;
}

input[type="checkbox"] {
  margin-right: 10px;
  cursor: pointer;
}

button {
  padding: 6px 12px;
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #d32f2f;
}
</style>


  <script>
  export default {
    name: 'TodoTask',
    props: ['task'],
    created() {
        console.log(this.task);
    },
    methods: {
      emitDeleteTask() {
        this.$emit('delete-task', this.task.id);
      }
    }
  };
  </script>  