<template>
    <header>
        <h1 id="title">
            {{ title }}
        </h1>
        <Button @click="$emit('show-addTask')" :text="showAddTask? 'Close' : 'Add Task'" :color="showAddTask ? 'maroon' : 'green'"/>
    </header>
</template>

<script>

    import Button from './Button.vue'

    export default {
        name: 'Header',
        props: {
            'title': String,
            'showAddTask': Boolean
        },
        components: {
            Button
        },
        emits: ['show-addTask']
    }
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 20px;
    }

    /* h1 #title {
        font-weight: bold;
    } */
</style>
