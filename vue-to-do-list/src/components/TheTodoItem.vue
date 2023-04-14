<script>
export default {
    name: "TodoItem",
    props: [
        "todoItem"
    ],
    methods: {
        todoDone() {
            this.todoItem.completed = !this.todoItem.completed
        }
    }
}
</script>
<template>
    <div class="container">
        <div v-bind:class="{ 'completed' : todoItem.completed }">
            <p>{{ todoItem.contributor }} : {{ todoItem.name }} ({{ todoItem.hours }})</p>
        </div>
        <button class="done-btn" v-if="!todoItem.completed" @click="todoDone">Done</button>
        <button class="edit-btn" v-if="!todoItem.completed" @click="editTodo">Edit</button>
        <button 
            class="delete-btn" 
            v-if="!todoItem.completed" 
            @click="$emit('delete-todo-event', todoItem.id)">
            Delete
        </button>
    </div>
</template>
<style scoped>
    .completed {
        text-decoration: line-through;
    }
</style>