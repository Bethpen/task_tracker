<template>
    <div v-for="task in tasks" :key='task.id'>
        <Task @togglereminder="$emit('togglereminder', task.id)" @delete-task="$emit('delete-task', task.id)" :task="task" />
    </div>
</template>

<script>
import Task from './Task.vue';

    export default{
        names: "Tasks",
        components: { Task },
        props:{
            tasks: Array,
        },
        emits: ['delete-task', 'togglereminder']
    }
        
</script>