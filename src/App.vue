<template>
<div class="container">
  <Header @show-addTask="toggleShowAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
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
      localStorage.setItem("todoItems", JSON.stringify(this.tasks))
    },
    toggleReminder(id){
      console.log(id);
      this.tasks = this.tasks.map(task => task.id == id ? {...task, reminder: !task.reminder} : task)
    },
    addTask(newTask){
      this.tasks = [...this.tasks, newTask]
    },
    toggleShowAddTask(){
      this.showAddTask = !this.showAddTask
    }
  },
  created(){

    if(localStorage.getItem("todoItems") === null){
        localStorage.setItem("todoItems", []);
         this.tasks = []
         this.toggleShowAddTask()
    } else {
      if(localStorage.getItem("todoItems")){
        this.tasks = JSON.parse(localStorage.getItem("todoItems"))
      } else {
        this.tasks = []
        this.toggleShowAddTask()
      }
      
    }
    
    if(typeof(Notification) !== undefined){
          Notification.requestPermission().then(permission => {
            if(permission){
              let title = "Welcome to Task Tracker!"
              let text = "We'll send notifications to remind you to complete your tasks :)"
              new Notification(title, {body: text})
            }
          })
    }

  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Inter', sans-serif;
  background-color: rgba(217,236,255);
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  padding: 30px;
  border-radius: 5px;
  box-shadow: 1px 2px 12px #606266;
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
