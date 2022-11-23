<template>
    <div class="job-item">
            <p class="job-name">{{job.name}}</p>
            <div class="function">
                <button @click="beforeEdit($event, job)">Edit</button>
                <button @click="removeJob($event, job)">Remove</button>
            </div>
        </div>
</template>

<script>
    export default {
        data() {
            return {}
        },
        props: {
            job: {
                type: Object,
                requered: true
            }
        },
        methods: {
            removeJob($event, job) {
                this.$emit("removeJob", job)
            },
            beforeEdit($event, job) {
                this.$emit("beforeEdit", job)
          },
        },
        mounted() {
            console.log("Mounted in JobItem")
        }
    }
</script>