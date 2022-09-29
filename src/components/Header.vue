<template>
  <div>
        <h1>{{title}}</h1>
        <Button v-show="homePage" @click="$emit('toggle-form')" :text="taskform ? 'Close' : 'Add task'" :color="taskform ? 'red' : 'green'"/>
  </div>
    
</template>

<script>
    import Button from './Button.vue';

    export default{
        name: 'header',
        components: {
            Button
        },
        props: {
            title: String,
            taskform: Boolean
        },
        computed:{
            homePage(){
                if(this.$route.path === '/'){
                    return true;
                }else{
                    return false
                }
            }
        }
    }
</script>

<style scoped>
header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>