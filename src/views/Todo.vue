<template>
    <div>
        <TodoList></TodoList>
    </div>
</template>

<script>
    import TodoList from '@/components/TodoList.vue'
    export default {
        name: "todo",
        components: {
            TodoList
        }
    }
</script>

<style scoped>

</style>