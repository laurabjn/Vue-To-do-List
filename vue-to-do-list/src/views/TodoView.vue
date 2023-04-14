<script>
import TheTodoFormVue from '../components/TheTodoForm.vue';
import TheTodoListVue from '../components/TheTodoList.vue';
import TheCountTodoVue from '../components/TheCountTodo.vue';

export default {
    name: 'App',
    components: {
        TheTodoFormVue, 
        TheTodoListVue,
        TheCountTodoVue
    },
    data() {
        return {
            todosList: [],
            count: 0
        }
    },
    methods: {
        addToDoItem(newTodo) {
            this.todosList = [...this.todosList, newTodo]
            this.count++
            console.log(this.todosList)
        },
        deleteTodo(id) {
            this.todosList = this.todosList.filter(todo => todo.id !== id)
            this.count--
            console.log(this.todosList)
        },
        editTodo(id) {
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
                @edit-todo-event="editTodo"
                @delete-todo-event="deleteTodo" />
        </div>
        <div class="count-to-do">
            <p>There is actually : </p>
            <TheCountTodoVue v-bind:countTodo="count"  />
        </div>
    </div>
</template>
<style scoped>
    .to-do-form {
        margin-top: 30px
    }
    .count-to-do {
        margin-top: 30px;
    }
</style>