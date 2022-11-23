<template>
    <div class="job-item">
        <p>Filter:</p>
        <div class="form">
            <input type="text" v-model="filter" name="" id="" @change="filterJobs">
            <button @click="filterJob">Filter</button>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                filter: ""
            }
        },
        methods: {
            filterJobs() {
                this.filterName = this.filter;
            }
        }, 
        mounted() {
            console.log("Mounted In FilterJob")
        }
    }
</script>