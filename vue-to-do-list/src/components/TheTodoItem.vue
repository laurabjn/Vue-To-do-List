<!-- eslint-disable vue/no-mutating-props -->
<script>
export default {
    name: "TodoItem",
    props: [
        "todoItem",
        "mode"
    ],
    methods: {
        todoDone() {
            this.todoItem.completed = !this.todoItem.completed
            this.$emit("done-todo-event", this.todoItem.completed);
        }
    }
}
</script>
<template>
    <div class="container">
        <div class="item" 
            v-bind:class="{ 'completed' : todoItem.completed }" 
            style="{{ todoItem.isSelected ? { background-color: lightgray; } : {} }}" >
            <p @click="$emit('select-todo-event', todoItem.id)">{{ todoItem.contributor }} : {{ todoItem.name }} ({{ todoItem.hours }} hour(s))</p>
        </div>
        <button class="done-btn" v-if="!todoItem.completed" @click="todoDone">Done</button>
        <button 
            class="edit-btn" 
            v-if="!todoItem.completed" 
            @click="$emit('edit-todo-event', todoItem.id)">
            Edit
        </button>
        <button 
            class="delete-btn" 
            v-if="!todoItem.completed" 
            @click="$emit('delete-todo-event', todoItem.id)">
            Delete
        </button>
    </div>
</template>
<style scoped>
    .item {
        color: black;
    }
    .item :hover {
        cursor: pointer;
        background-color: lightgray;
    }
    .completed {
        text-decoration: line-through;
    }
</style>