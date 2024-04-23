<!-- eslint-disable vue/no-deprecated-filter -->
<template>
    <div class="elevator-details">
      <h1>Elevator Details</h1>
      <div v-if="loading" class="loader">Loading...</div>
      <div v-if="error" class="error-message">An error occurred: {{ error }}</div>
      <div v-if="elevator" class="details">
        <h2>{{ elevator.location }}</h2>
        <p>Status: {{ elevator.status }}</p>
        <p>Last Maintenance: {{ elevator.lastMaintenance | formatDate }}</p>
        <p>Next Scheduled Maintenance: {{ elevator.nextMaintenance | formatDate }}</p>
        <div v-for="alert in elevator.alerts" :key="alert.id" class="alert">
          <p>{{ alert.message }}</p>
          <p>Date: {{ alert.date | formatDate }}</p>
        </div>
        <!-- Add more details as needed -->
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        elevator: null,
        loading: false,
        error: null
      };
    },
    filters: {
      formatDate(value) {
        if (value) {
          return new Date(value).toLocaleDateString();
        }
      }
    },
    created() {
      this.fetchElevatorDetails();
    },
    methods: {
      fetchElevatorDetails() {
        this.loading = true;
        const id = this.$route.params.id;
        axios.get(`/api/elevators/${id}`)
          .then(response => {
            this.elevator = response.data;
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
  .elevator-details {
    padding: 2rem;
  }
  
  h1 {
    text-align: center;
    margin-bottom: 2rem;
  }
  
  .details {
    border: 1px solid #eaeaea;
    border-radius: 8px;
    padding: 1rem;
    margin-bottom: 1rem;
  }
  
  .alert {
    background-color: #ffcccc;
    border-left: 5px solid #ff0000;
    padding: 0.5rem;
    margin-bottom: 1rem;
  }
  
  .loader,
  .error-message {
    text-align: center;
    margin-top: 2rem;
  }
  
  @media (max-width: 768px) {
    .elevator-details {
      padding: 1rem;
    }
  }
  </style>
  