<script>
import {v4 as uuidv4} from 'uuid';

export default {
    name: "TodoForm",
    data() {
        return {
            name: '',
            hours: 0,
            contributor: ''
        }
    },
    methods: {
        //Add a new Task
        SubmitTask(event) {
            event.preventDefault();

            const newTaskObject = {
                id: uuidv4(),
                name: this.name,
                hours: this.hours,
                contributor: this.contributor,
                completed: false
            }
            console.log(newTaskObject)
            this.$emit("submit-task-event", newTaskObject);
            this.name = ''
            this.hours = 0
            this.contributor = ''
        } 
    }
}
</script>
<template>
    <div>
        <form @submit="SubmitTask">
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
            <select name="contributors" id="contributor-select" v-model="contributor">
                <option value="">Contributor</option>
                <option value="alice">Alice</option>
                <option value="bob">Bob</option>
            </select>
            <button class="add-btn" type="submit">Add</button>
        </form>
    </div>
</template>