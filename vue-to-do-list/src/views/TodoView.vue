<script>
import TheTodoFormVue from '../components/TheTodoForm.vue';
import TheTodoListVue from '../components/TheTodoList.vue';

export default {
    name: 'App',
    components: {
        TheTodoFormVue, 
        TheTodoListVue
    },
    data() {
        return {
            todosList: []
        }
    },
    methods: {
        addToDoItem(newTodo) {
            this.todosList = [...this.todosList, newTodo]
            console.log(this.todosList)
        },
        deleteTodo(id) {
            this.todosList = this.todosList.filter(todo => todo.id !== id)
            console.log(this.todosList)
        }
    }
}
</script>
<template>
    <div class="container">
        <h1 class="title"> My Todo List</h1>
        <div class="to-do-form">
            <TheTodoFormVue @submit-task-event="addToDoItem" />
        </div>
        <div class="to-dos-list">
            <TheTodoListVue 
                v-bind:todoList="todosList"
                @delete-todo-event="deleteTodo" />
        </div>
    </div>
</template>
<style scoped>

</style>