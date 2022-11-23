<template>
  <add-job v-on:addJob="saveJob"></add-job>
      <filter-job v-on:filterJobs="filterJobsByName"></filter-job>
      <div class="list-job">
        <div class="edit-job">
          <p class="label">Edit:</p>
          <input type="text" v-model="editJob.name" name="" id="">
          <button @click="updateJob">Save</button>
        </div>
        <job-item v-on:removeJob="removeJob" v-on:beforeEdit="beforeEditJob" v-for="jobItem in getJobs" :job="jobItem" :key="jobItem.id"></job-item>
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
            jobs: [
              {
                id: 1,
                name: 'Job 1'
              },
              {
                  id: 4, 
                  name: 'Job 4'
              },
              {
                  id: 2, 
                  name: 'Job 2'
              },
              {
                  id: 3, 
                  name: 'Job 3'
              }
          ],
          editJob: {},
          filterName: ""
        }
      }
      , methods: {
        updateJob() {
          if(this.editJob) {
              this.jobs[this.editJob.id - 1] = {... this.editJob}
              this.editJob.name = ''
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
        }, 
        filterJobsByName(name) {
          this.filterName = name
        }
      }, 
      computed: {
        getJobs() {
          console.log(this.j)
          let filterJobs;
          if(this.name !== '') {
            filterJobs = this.jobs.filter(job => job.name.toLowerCase().match(this.filterName.toLowerCase()))
          }else filterJobs = this.jobs;
          filterJobs.sort((a, b) => a.name.localeCompare(b.name))
          return filterJobs;
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
  * {
    font-size: 18px;
    margin: 0;
    padding: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
  #app {
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }

 .add-job, .list-job, .filter-job {
  padding: 10px 20px;
  border-radius: 10px;
  border: .5px solid #ccc;
  width: 380px;
 }

 .add-job {
  margin-bottom: 15px;
 }

 .add-job .form {
  display: flex;
  align-items: center;
  margin-top: 10px;
  justify-content: space-between;
 }

 input, button {
  border-radius: 5px;
  padding: 5px 5px;
  min-width: 60px;
  margin-right: 5px;
  border: .5px solid #ccc;
 }

 .edit-job, .filter-job {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 15px;
 }

  .job-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 15px;
  }
</style>
