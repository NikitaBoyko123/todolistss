<template>
  <div class="app">
    <h1>Add a new task</h1>
    
    <div class="task-section">
      <h2>Tasks to do - {{ pendingTasks.length }}</h2>
      <ul>
        <li v-for="(task, index) in pendingTasks" :key="index">
          {{ task.text }}
          <span class="task-actions">
            <button @click="completeTask(index)" class="complete-btn">✓</button>
            <button @click="deleteTask(index, 'pending')" class="delete-btn">☐</button>
          </span>
        </li>
      </ul>
    </div>
    
    <div class="task-section">
      <h2>Done - {{ completedTasks.length }}</h2>
      <ul>
        <li v-for="(task, index) in completedTasks" :key="index">
          {{ task.text }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      tasks: [
        { text: 'To study React fundamentals', completed: false },
        { text: 'To study React fundamentals', completed: false },
        { text: 'To study React fundamentals', completed: false },
        { text: 'To study React fundamentals', completed: false },
        { text: 'To study React fundamentals', completed: true }
      ]
    }
  },
  computed: {
    pendingTasks() {
      return this.tasks.filter(task => !task.completed);
    },
    completedTasks() {
      return this.tasks.filter(task => task.completed);
    }
  },
  methods: {
    completeTask(index) {
      this.tasks = this.tasks.map((task, i) => {
        if (i === index) {
          return { ...task, completed: true };
        }
        return task;
      });
    },
    deleteTask(index, type) {
      if (type === 'pending') {
        const taskIndex = this.tasks.findIndex(task => 
          !task.completed && task.text === this.pendingTasks[index].text
        );
        if (taskIndex !== -1) {
          this.tasks.splice(taskIndex, 1);
        }
      }
    }
  }
}
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #f5f5f5;
  margin: 0;
  padding: 20px;
}

.app {
  max-width: 600px;
  margin: 0 auto;
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h1 {
  font-size: 24px;
  margin-bottom: 20px;
  color: #333;
}

h2 {
  font-size: 18px;
  margin: 15px 0 10px 0;
  color: #555;
}

.task-section {
  margin-bottom: 25px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  padding: 8px 0;
  border-bottom: 1px solid #eee;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task-actions {
  display: flex;
  gap: 5px;
}

button {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 16px;
  padding: 2px 5px;
}

.complete-btn {
  color: #4CAF50;
}

.delete-btn {
  color: #F44336;
}

button:hover {
  opacity: 0.8;
}
</style>
