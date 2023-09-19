<template>
  <div class="home">
    <!-- <input type="text" value = {{searchFilter}} onChange={{(event) => searchFilter = event.target.value}}/> -->
    <h1>{{ message }}</h1>
    <button v-on:click="sortedSchools">button</button>
    <div v-for="school in schools">
      <p>{{ school[9] }}</p>
      <button v-on:click="showSchool(school)">More Info </button>
      <hr />
    </div>
    <dialog id="school-details" >
    <form method="dialog">
      <p> Avgerage math score: {{ currentSchool[12] }}</p>
      <p> Average enlgish score: {{ currentSchool[13] }}</p>
      <button>Close</button>
    </form>
    </dialog>
  </div>
</template>
<style>
</style>

<script>
import axios from 'axios';

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      schools: [],
      searchFilter: "",
      currentSchool: {},
      sortedSchools: [],
    };
  },
  created: function() {
    this.getData()
  },
  methods: {
    getData: function() {
      console.log('get data')
      axios.get("https://data.cityofnewyork.us/api/views/f9bf-2cp4/rows.json").then(response => {
        console.log(response.data)
        this.schools = response.data.data
      })
    },
    showSchool: function(school) {
      this.currentSchool = school
      document.querySelector("#school-details").showModal();
    },
    
  }
}
  
;
</script>