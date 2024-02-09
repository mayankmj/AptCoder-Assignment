<template>
  <div class="task-grid">

    <div class="task-column">
      <h2 class="section-heading">Open Tasks</h2>
      <ul class="task-list">
        <li v-for="task in openTasks" :key="task.id">
          <span class="task-title">{{ task.title }}</span>
          <span class="task-details">Created on {{ formatDate(task.createdAt) }}</span>
          <button @click="completeTask(task.id)" class="complete-button">Complete</button>
        </li>
      </ul>
    </div>


    <div class="task-column">
      <h2 class="section-heading">Completed Tasks</h2>
      <ul class="task-list">
        <li v-for="task in completedTasks" :key="task.id">
          <span class="task-title">{{ task.title }}</span>
          <span class="task-details">Completed </span>
        </li>
      </ul>
    </div>
  </div>
</template>



<script>
export default {
  props: ['tasks'],
  methods: {
    formatDate(date) {
      
      return new Date(date).toLocaleString();
    },
    completeTask(id) {
      this.$emit('completeTask', id);
    }
  },
  computed: {
    openTasks() {
      return this.tasks.filter(task => !task.completed);
    },
    completedTasks() {
      return this.tasks.filter(task => task.completed);
    }
  }
}
</script>

<style scoped>

.section-heading {
  font-size: 1.5em;
  color: #333;
  margin-bottom: 10px;
}
.task-column {
  padding-right: 30px;
}
.task-grid {
  display: grid;
  grid-template-columns: 1fr 1fr; 
  gap: 20px; 
}

.task-list {
  list-style-type: none;
  padding: 0;
}

li {
  background-color: #f4f4f4;
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task-title {
  font-weight: bold;
}

.task-details {
  color: #777;
}

.complete-button {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
}
</style>
