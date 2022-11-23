<template>
    <div class="add-job">
        <p>New todo:</p>
        <div class="form">
            <input ref="input" type="text" v-model="newJob" name="" id="" :placeholder="notiMessage">
            <button @click="addJob()">Add</button>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                id: 3,
                newJob: "",
                notiMessage: "Enter new job"
            }
        },
        methods: {
            addJob() {
                if(this.newJob === '') {
                    this.notiMessage = "Job can't blank"
                    this.$refs.input.focus()
                }else {
                    this.$emit('addJob', {id: this.id++, name: this.newJob})
                }
          },
        }, 
        mounted() {
            this.$refs.input.focus()
            console.log("Mounted In AddJob")
        }
    }
</script>