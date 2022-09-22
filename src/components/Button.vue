<template>
    <button class="btn" :style="{background: color}">{{text}}</button>
</template>

<script>

    export default{
        name: 'button',
        props: {
            text: String,
            color: String
        }
    }
</script>