<template>
  <body>
    <div id="app">
      <h2>Task List</h2>
      <ul>
        <li v-for="(task, index) in tasks" :key="index">{{ task }}</li>
      </ul>
      <form @submit="addTask">
        <input type="text" v-model="newTask" placeholder="Add a new task">
        <button type="submit">Add</button>
      </form>
      <form @submit="removelastTask">
        <button type="submit">remove</button>
      </form>
    </div>
  </body>
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
      newTask: '',
    };
  },
  created() {
    const savedTasks = localStorage.getItem('tasks');
    if (savedTasks) {
      this.tasks = JSON.parse(savedTasks);
    }
  },
  methods: {
    addTask(event) {
      event.preventDefault();

      if (this.newTask.trim() !== '') {
        this.tasks.push(this.newTask);
        this.newTask = '';

        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      }
    },
    removelastTask(event) {
      event.preventDefault();
        this.tasks.pop(this.newTask);
        this.newTask = '';

        localStorage.setItem('tasks', JSON.stringify(this.tasks));
    }
  },
};
</script>
