<template>
    <div class="browse-elevators">
      <h1>Browse Elevators</h1>
      <div v-if="loading" class="loader">Loading...</div>
      <div v-if="error" class="error-message">An error occurred: {{ error }}</div>
      <div v-for="elevator in elevators" :key="elevator.ElevatorID" class="elevator-card">
        <h2>{{ elevator.Location }}</h2>
        <p>Status: {{ elevator.Status }}</p>
        <router-link :to="'/elevator-details/' + elevator.ElevatorID">View Details</router-link>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        elevators: [],
        loading: false,
        error: null
      };
    },
    mounted() {
      this.fetchElevators();
    },
    methods: {
      fetchElevators() {
        this.loading = true;
        axios.get('/api/elevators')
          .then(response => {
            this.elevators = response.data;
            this.loading = false;
          })
          .catch(error => {
            this.error = error.message;
            this.loading = false;
          });
      }
    }
  };
  </script>
  
  <style>
  .browse-elevators {
    padding: 2rem;
  }
  
  .h1 {
    text-align: center;
    margin-bottom: 2rem;
  }
  
  .elevator-card {
    border: 1px solid #eaeaea;
    border-radius: 8px;
    padding: 1rem;
    margin-bottom: 1rem;
    transition: box-shadow 0.3s ease;
  }
  
  .elevator-card:hover {
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  }
  
  .loader,
  .error-message {
    text-align: center;
    margin-top: 2rem;
  }
  </style>
  