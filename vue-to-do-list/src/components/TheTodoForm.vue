<!-- eslint-disable vue/no-mutating-props -->
<script>
import { v4 as uuidv4 } from 'uuid';

export default {
    name: "TodoForm",
    props: [
        "editing",
        "todoEdit"
    ],
    data() {
        return {
            name: "",
            hours: 0,
            contributor: "",
            errors: []
        }
    },
    mounted() {
        console.log(this.todoEdit)
        if (this.editing) {
            console.log(this.todoEdit)
            this.name = this.todoEdit.name
            this.hours = this.todoEdit.hours
            this.contributor = this.todoEdit.contributor
        }
    },
    methods: {
        checkForm() {
            if (this.name && this.hours && this.contributor) {
                this.errors = []
                return true
            }

            this.errors = []

            if (!this.name) {
                this.errors.push('Name required.')
            }

            if (!this.hours) {
                this.errors.push('Hours required.')
            }

            if (this.hours > 0) {
                this.errors.push('Hours must be grater than 0.')
            }

            if (!this.contributor) {
                this.errors.push('Contributor required.')
            }

            return false
        },
        //Add a new Task
        SubmitTask(event) {
            event.preventDefault();

            if (this.checkForm()) {
                if (!this.editing) {
                    const newTaskObject = {
                        id: uuidv4(),
                        name: this.name,
                        hours: this.hours,
                        contributor: this.contributor,
                        completed: false
                    }

                    this.$emit("submit-task-event", newTaskObject);
                    this.name = ''
                    this.hours = 0
                    this.contributor = ''
                } else {
                    const taskEdit = {
                        id: this.todoEdit.id,
                        name: this.name,
                        hours: this.hours,
                        contributor: this.contributor,
                        completed: false
                    }
                    console.log(taskEdit)

                    if (taskEdit.name != "" && taskEdit.hours != 0 
                        && taskEdit.hours > 0 && taskEdit.contributor != "") {
                        this.$emit("submit-task-event", taskEdit);
                        this.name = ''
                        this.hours = 0
                        this.contributor = ''
                    } 
                }
            }
        } 
    }
}
</script>
<template>
    <div>
        <form class="form-to-do" @submit="SubmitTask">
            <p class="error" v-if="errors.length">
                <b>Please correct the following error(s) : </b>
                <ul>
                    <li v-bind:key="error.id" v-for="error in errors">{{ error }}</li>
                </ul>
            </p>
            <input  type="text"
                    class="input-name"
                    v-model="name"
                    placeholder="Name of the task"
            />
            <input  type="number"
                    class="input-hours"
                    v-model="hours"
                    placeholder="0"
            />
            <select 
                class="select-contributors" 
                name="contributors" 
                id="contributor-select" 
                v-model="contributor">
                <option value="">Contributor</option>
                <option value="alice">Alice</option>
                <option value="bob">Bob</option>
            </select>
            <button class="add-btn" type="submit" v-if="!editing">Add</button>
            <button class="edit-btn" type="submit" v-if="editing">Edit</button>
        </form>
    </div>
</template>
<style scoped>
    .error {
        color: red;
    }
    .input-name {
        margin-right: 10px;
    }
    .input-hours {
        margin-right: 10px;
        width: 50px;
    }
    .select-contributors {
        margin-right: 10px;
        width: 100px;
    }
    .add-btn {
        margin-right: 10px;
        width: 70px;
    }
</style>