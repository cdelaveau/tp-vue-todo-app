<template>
  <div class="home">
    <h1>Bienvenue dans l'application To-Do</h1>
    <p>Gérez vos tâches quotidiennes de manière efficace et intuitive.</p>
    <todo-list></todo-list>
  </div>
</template>

<script>
import ToDoList from '@/components/ToDoList.vue';

export default {
  name: 'HomeView',
  components: {
    'todo-list': ToDoList
  }
};
</script>

<style scoped>
.home h1 {
  color: #35495e;
  margin-bottom: 20px;
}

.home p {
  color: #627c91;
  font-size: 16px;
}
</style>
