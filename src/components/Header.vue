<template>
    <div class="container">
        <h1>{{title}}</h1>
    </div>
    <Button text="Add task" color="green"/>
</template>

<script>
    import Button from './Button.vue';

    export default{
        name: 'header',
        components: {
            Button
        },
        props: {
            title: String
        }
    }
</script>