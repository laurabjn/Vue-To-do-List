<script>
import {v4 as uuidv4} from 'uuid';

export default {
    name: "TodoForm",
    props: ["editing", "todoEdit"],
    data() {
        return {
            name: this.todoEdit.name,
            hours: this.todoEdit.hours,
            contributor: this.todoEdit.contributor
        }
    },
    methods: {
        //Add a new Task
        SubmitTask(event) {
            event.preventDefault();

            if (!this.editing) {
                const newTaskObject = {
                    id: uuidv4(),
                    name: this.name,
                    hours: this.hours,
                    contributor: this.contributor,
                    completed: false
                }
                console.log(newTaskObject)

                if (newTaskObject.name != "" && newTaskObject.hours != 0 
                    && newTaskObject.hours > 0 && newTaskObject.contributor != "") {
                    this.$emit("submit-task-event", newTaskObject);
                    this.name = ''
                    this.hours = 0
                    this.contributor = ''
                } 
            } else {
                const taskEdit = {
                    id: this.id,
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
</script>
<template>
    <div>
        <form class="form-to-do" @submit="SubmitTask">
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
            <select class="select-contributors" name="contributors" id="contributor-select" v-model="contributor">
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