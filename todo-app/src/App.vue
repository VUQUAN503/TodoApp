<template>
  <div id="app">
      <add-job v-on:addJob="saveJob"></add-job>
      <filter-job :filterName="filterByName"></filter-job>
      <div class="list-job">
      <div class="job-item">
          <p class="label">Edit:</p>
          <input type="text" v-model="editJob.name" name="" id="">
          <button @click="updateJob">Save</button>
      </div>
      <job-item v-on:removeJob="removeJob" v-on:beforeEdit="beforeEditJob" v-for="jobItem in jobs" :job="jobItem" :key="jobItem.id"></job-item>
      </div>
  </div>
</template>

<script>
  import JobItem from "./components/JobItem.vue";
  import FilterJob from "./components/FilterJob.vue";
  import AddJob from "./components/AddJob.vue";

  export default {
      components: {
          JobItem,
          FilterJob,
          AddJob
      },
      data() {
          return {
            jobs: [{id: 1
              , name: 'Job 1'},
              {
                  id: 2, 
                  name: 'Job 2'
              },
          ],
          editJob: {},
          filterByName: ""
        }
      }
      , methods: {
        updateJob() {
          if(this.editJob) {
              this.jobs[this.editJob.id - 1] = {... this.editJob}
          }
        },
        saveJob(job) {
            this.jobs.push(job)
        },
        beforeEditJob(job) {
          this.editJob = {... job}
        },
        removeJob(job) {
          this.jobs.splice(this.jobs.indexOf(job), 1)
        }
      }, 
      mounted() {
        console.log("Mounted In App")
      },
      beforeCreate() {
        console.log('Before create')
      }, 
      created() {
        console.log('Created')
      }
  }
</script>

<style>
  .job-item {
    display: flex;
    align-items: center;
  }

  .job-name {
    margin-right: 30px;
  }
</style>
