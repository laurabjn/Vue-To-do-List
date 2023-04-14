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
            <li v-bind:key="todo.id" v-for="todo in todos">
                <TheTodoItemVue 
                    v-bind:todoItem="todo" 
                    @delete-todo-event="$emit('delete-todo-event', todo.id)" />
            </li>
        </ul>
    </div>
</template>