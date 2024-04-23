<template>
    <div class="search-elevators">
      <h1>Search Elevators</h1>
      <div class="search-bar">
        <input type="text" v-model="searchQuery" placeholder="Search elevators..." @input="fetchSearchResults" />
        <select v-model="selectedRegion" @change="fetchSearchResults">
          <option value="">All Regions</option>
          <option v-for="region in regions" :key="region" :value="region">{{ region }}</option>
        </select>
        <select v-model="selectedStatus" @change="fetchSearchResults">
          <option value="">All Statuses</option>
          <option v-for="status in statuses" :key="status" :value="status">{{ status }}</option>
        </select>
      </div>
      <div v-if="loading" class="loader">Loading...</div>
      <div v-if="error" class="error-message">An error occurred: {{ error }}</div>
      <div v-for="elevator in searchResults" :key="elevator.ElevatorID" class="elevator-result">
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
        searchQuery: '',
        selectedRegion: '',
        selectedStatus: '',
        searchResults: [],
        regions: ['Region 1', 'Region 2', 'Region 3'], // Replace with actual regions from your database
        statuses: ['Operational', 'Maintenance', 'Out of Service'], // Replace with actual statuses from your database
        loading: false,
        error: null
      };
    },
    methods: {
      fetchSearchResults() {
        this.loading = true;
        const params = new URLSearchParams({
          search: this.searchQuery,
          region: this.selectedRegion,
          status: this.selectedStatus
        }).toString();
        axios.get(`/api/search-elevators?${params}`) // Replace with your actual search endpoint
          .then(response => {
            this.searchResults = response.data;
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
  .search-elevators {
    padding: 2rem;
  }
  
  h1 {
    text-align: center;
    margin-bottom: 2rem;
  }
  
  .search-bar {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-bottom: 2rem;
  }
  
  .search-bar input,
  .search-bar select {
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  
  .elevator-result {
    border: 1px solid #eaeaea;
    border-radius: 8px;
    padding: 1rem;
    margin-bottom: 1rem;
    transition: box-shadow 0.3s ease;
  }
  
  .elevator-result:hover {
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  }
  
  .loader,
  .error-message {
    text-align: center;
    margin-top: 2rem;
  }
  
  @media (max-width: 768px) {
    .search-bar {
      flex-direction: column;
    }
  }
  </style>
  