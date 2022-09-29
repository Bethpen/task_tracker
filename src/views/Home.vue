<template>
    <AddTask v-show="taskform" @add-task='addTask' />
    <Tasks @togglereminder="toggleReminder" @delete-task="deletetask" :tasks="tasks"/>
    
</template>

<script>
import AddTask from '../components/AddTask.vue';
import Tasks from '../components/Tasks.vue';
    export default{
        name: 'Home',
        data(){
         return{
            tasks: []
         }
        },
        props:{
            taskform: Boolean
        },
        components:{
            AddTask,
            Tasks
        },
        methods:{
        async addTask(task){
            const res = await fetch('http://localhost:5000/tasks', {
            method: 'POST',
            headers:{
                'content-type': 'application/json'
            },
            body: JSON.stringify(task)
            })

            const data = await res.json();

            this.tasks = [...this.tasks, data]
        },
        async deletetask(id){
            if(confirm('Are you sure?')){
            const res = await fetch(`http://localhost:5000/tasks/${id}`, {
                method: 'DELETE'
            })

            res.status === 200 ? (this.tasks = this.tasks.filter((task)=> task.id !== id)): alert('There was an error deleting the task')
            }
        },
        async toggleReminder(id){
            const taskToToggle = await this.fetchTask(id)
            const updtask = {...taskToToggle, reminder: !taskToToggle.reminder}

            const res = await fetch(`http://localhost:5000/tasks/${id}`, {
            method: 'PUT',
            headers:{
                'content-type': 'application/json'
            },
            body: JSON.stringify(updtask)
            })

            const data = await res.json()

        this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: updtask.reminder} : task) 
        },
        async fetchTasks(){
            const res = await fetch('http://localhost:5000/tasks');
            const data = await res.json();
            return data;
        },
        async fetchTask(id){
            const res = await fetch(`http://localhost:5000/tasks/${id}`);
            const data = await res.json();
            return data;
        }
    },
        async created(){
        this.tasks =  await this.fetchTasks();
        }   
    }
</script>

<style>

</style>