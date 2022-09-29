<template>
    <div @dblclick="$emit('togglereminder', task.id)" :class="[task.reminder? 'reminder': '', 'task']">
        <h3>{{task.text}}
          <iconify-icon @click="$emit('delete-task', task.id)" class="icon" icon="humbleicons:times"></iconify-icon>
        </h3>
        <p>{{task.day}}</p>
    </div>
</template>

<script>
    export default{
        name: 'Task',
        props: {
            task: Object
        }
    }
</script>

<style>
.icon {
  color: red;
  border: none;
  outline: none;
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