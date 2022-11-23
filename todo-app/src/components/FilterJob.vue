<template>
    <div class="filter-job">
        <p>Filter:</p>
        <div class="form">
            <input type="text" v-model="filterName" name="" id="" @input="filterJob">
            <button @click="filterJob">Filter</button>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                filterName: ""
            }
        },
        methods: {
            filterJob() {
                this.$emit('filterJobs', this.filterName)
            }
        }, 
        mounted() {
            console.log("Mounted In FilterJob")
        }
    }
</script>