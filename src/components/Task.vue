<template>
    <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '']">
        <h3>
            {{ task.text }}
            <i class="fas fa-times" @click="$emit('delete-task', task.id)"></i>
        </h3>
        <p class="info">
            {{ task.day }}
            {{ task.time }}
        </p>
    </div>
</template>

<script>

    export default {
        name: 'Task',
        props: {
            task: Object,
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
  border-radius: 5px;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.task .info {
  font-size: .9rem;
}
</style>
