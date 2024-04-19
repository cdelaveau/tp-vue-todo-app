<template>
    <div>
      <h2>Ma liste de tâches</h2>
      <table v-if="tasks.length">
        <todo-task
          v-for="task in tasks"
          :key="task.id"
          :task="task"
          @delete-task="deleteTask"
        ></todo-task>
      </table>
      <p v-else>Aucune tâche à afficher.</p>
    </div>
</template>
  
  
<script>
  import TodoTask from './TodoTask.vue';
  import axios from 'axios';
  
  export default {
    name: 'ToDoList',
    components: {
      TodoTask
    },
    data() {
      return {
        tasks: []
      };
    },
    mounted() {
      this.loadTasks();
    },
    methods: {
      loadTasks() {
        axios.get('https://jsonplaceholder.typicode.com/todos')
          .then(response => {
            this.tasks = response.data.slice(0, 20);
          })
          .catch(error => {
            console.error("Erreur pendant le chargement des tâches :", error);
          });
      },
      deleteTask(taskId) {
        this.tasks = this.tasks.filter(task => task.id !== taskId);
      }
    }
  };
</script>
  