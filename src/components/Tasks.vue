<template>
    <div :key="task.id" v-for="task in tasks">
        <h3>
            <Task @dblclick="$emit('toggle-reminder', task.id)" @deleteTask="$emit('delete-task', task.id)" :task="task" class="task"/>
        </h3>
    </div>
</template>

<script>

import Task from './Task'
export default {
    name: 'Tasks',
    props: {
        tasks: Array
    },
    components: {
        Task
    },
    emits: ['delete-task', 'toggle-reminder']
}
</script>

<style scope>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>