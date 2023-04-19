<script>
import TheTodoItemVue from './TheTodoItem.vue';

export default {
    name: "TodoList",
    props: [
        "todoList"
    ],
    components: {
        TheTodoItemVue
    }
}
</script>
<template>
    <div class="container">
        <ul class="todos-list">
            <li class="todo" v-bind:key="todo.id" v-for="todo in todoList">
                <TheTodoItemVue 
                    v-bind:todoItem="todo" 
                    @done-todo-event="$emit('done-todo-event', todo.completed)"
                    @edit-todo-event="$emit('edit-todo-event', todo.id)"
                    @delete-todo-event="$emit('delete-todo-event', todo.id)" />
            </li>
        </ul>
    </div>
</template>
<style scoped>
    .todos-list {
        margin-top: 30px;
        width: 700px;
        height: 100px;
    }
</style>