<template>
  <div>
    <h1>Ma liste de tâches</h1>
    <p>Tâches complétées : {{ completedTasksCount }} sur {{ tasks.length }}</p>
    <div class="progress-bar">
      <div class="progress" :style="{ width: completionRate + '%' }"></div>
    </div>
    <table>
      <todo-task
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @delete-task="deleteTask"
      ></todo-task>
    </table>
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
  computed: {
    completedTasksCount() {
      return this.tasks.filter(task => task.completed).length;
    },
    completionRate() {
      const total = this.tasks.length;
      const completed = this.completedTasksCount;
      return total > 0 ? (completed / total) * 100 : 0;
    }
  },
  methods: {
    deleteTask(taskId) {
      this.tasks = this.tasks.filter(task => task.id !== taskId);
    }
  },
  mounted() {
    axios.get('https://jsonplaceholder.typicode.com/todos')
      .then(response => {
        this.tasks = response.data.slice(0, 10); // Limit to first 10 tasks for demo
      })
      .catch(error => {
        console.error("There was an error loading the tasks:", error);
      });
  }
};
</script>

<style scoped>
.progress-bar {
  width: 100%;
  background-color: #e0e0e0;
  border-radius: 8px;
  margin: 10px 0;
}

.progress {
  height: 20px;
  background-color: #76c7c0;
  border-radius: 8px;
  transition: width 0.3s ease-in-out;
}

table {
  width: 100%;
  border-collapse: collapse;
}

table td, table th {
  border: 1px solid #ddd;
  padding: 8px;
}

table tr:nth-child(even) {
  background-color: #f2f2f2;
}

table tr:hover {
  background-color: #ddd;
}
</style>
