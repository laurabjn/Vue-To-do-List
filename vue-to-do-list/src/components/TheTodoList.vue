<script>
import TheTodoItemVue from './TheTodoItem.vue';

export default {
    name: "TodoList",
    components: {
        TheTodoItemVue
    }
}
</script>
<template>
    <div class="container">
        <ul class="todos-list">
            <li class="todo" v-bind:key="todo.id" v-for="todo in todos">
                <TheTodoItemVue 
                    v-bind:todoItem="todo" 
                    @edit-todo-event="$emit('edit-todo-event', todo.id)"
                    @delete-todo-event="$emit('delete-todo-event', todo.id)" />
            </li>
        </ul>
    </div>
</template>
<style>
    .todos-list {
        margin-top: 30px;
        height: 100px;
        border: solid black;
    }
</style>