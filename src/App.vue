<template>
<div class="container">
  <Header @show-addTask="toggleShowAddTask" title="Task Tracker"/>
  <div v-show="showAddTask">
    <AddTask @add-task="addTask"/>
  </div>

  <Tasks @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks"/>
</div>
  <h3>
    
  </h3>
</template>

<script>

import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  methods: 
  {
    deleteTask(id){
      this.tasks = this.tasks.filter(task => task.id !== id)
    },
    toggleReminder(id){
      console.log(id);
      this.tasks = this.tasks.map(task => task.id == id ? {...task, reminder: !task.reminder} : task)
    },
    addTask(task){
      this.tasks = [...this.tasks, task]
    },
    toggleShowAddTask(){
      this.showAddTask = !this.showAddTask
    }
  },
  created(){
    this.tasks = [
      {
        id: 1,
        text: "Task 1",
        day: "02/21/2021",
        reminder: false
      },
      {
        id: 2,
        text: "Task 2",
        day: "02/24/2021",
        reminder: false
      },
      {
        id: 3,
        text: "Task 3",
        day: "03/11/2021",
        reminder: true
      }
    ]
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@200;300&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
