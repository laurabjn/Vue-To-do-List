<script>
import TheTodoListVue from '../components/TheTodoList.vue';
import TheCountTodoVue from '../components/TheCountTodo.vue';
import TheTodoFormVue from '../components/TheTodoForm.vue';

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
            todoSelectList: [],
            editing: false,
            todoEdit: {
                name: '',
                hours: 0,
                contributor: '',
            },
            count: 0,
            countInProgress: 0,
            countDone: 0
        }
    },
    methods: {
        addOrEditToDoItem(newTodo) {
            if (!this.editing) {
                this.todosList = [...this.todosList, newTodo]
                this.count++
                this.countInProgress++
            } else {
                this.todosList.forEach(todo => {
                    if (todo.id == newTodo.id) {
                        todo.name = newTodo.name
                        todo.hours = newTodo.hours
                        todo.contributor = newTodo.contributor
                    }
                });
                this.editing = false
                this.todoEdit = {}
            }
        },
        selectTodo(id) {
            this.todosList.forEach(todo => {
                if (todo.id == id) {
                    todo.isSelected = true
                }
            });

        },
        deleteTodo(id) {
            this.todosList = this.todosList.filter(todo => todo.id !== id)
            this.count--
            this.countInProgress--
        },
        deleteTodoSelected() {
            this.todosList = this.todosList.filter(todo => !todo.isSelected )
            if (this.count > 0) {
                this.count--
            }
            this.countInProgress--
        },
        edit(id) {
            this.editing = true
            this.todosList.forEach(todo => {
                if (todo.id == id) {
                    this.todoEdit = todo
                }
            });
            console.log(this.editing)
        },
        countDoneTodo(completed) {
            if (completed) {
                this.countDone++;
                this.countInProgress--;
            }
        }
    }
}
</script>
<template>
    <div class="container">
        <h1 class="title"> My Todo List</h1>
        <div class="to-do-form">
            <TheTodoFormVue 
                @submit-task-event="addOrEditToDoItem" 
                v-bind:todoEdit="todoEdit" 
                v-bind:editing="editing" />
        </div>
        <div class="to-dos-list">
            <TheTodoListVue 
                v-bind:todoList="todosList"
                @select-todo-event="selectTodo"
                @done-todo-event="countDoneTodo"
                @edit-todo-event="edit"
                @delete-todo-event="deleteTodo" />
        </div>
        <div class="count-to-do">
            <p>There is actually : </p>
            <TheCountTodoVue v-bind:countTodo="count"/>
            <div class="in-progress" v-if="todosList.length > 0">
                <p>{{ countInProgress }} in progress task</p>
            </div>
            <div class="done" v-if="todosList.length > 0">
                <p>{{ countDone }} task done</p>
            </div>
        </div>
        <div>
            <button @click="deleteTodoSelected">Delete todo selected</button>
        </div>
    </div>
</template>
<style scoped>
    .to-do-form {
        margin-top: 30px
    }
    .count-to-do {
        margin-top: 70px;
    }
</style>