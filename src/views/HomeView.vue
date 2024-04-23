<template>
  <div class="home">
    <h1 class="title">Welcome to the Elevator Monitoring System</h1>
    <p class="intro">
      Explore our cutting-edge solution for real-time elevator monitoring and ensure the safety and efficiency of your high-rise transportation.
    </p>
    <div class="card-container">
      <router-link to="/browse" class="card animate-fade-slide">
        <h2>Browse Elevators</h2>
        <p>View a list of all elevators and their current status.</p>
      </router-link>
      <router-link to="/search" class="card animate-fade-slide">
        <h2>Search Elevators</h2>
        <p>Find specific elevators with advanced search filters.</p>
      </router-link>
      <router-link to="/view" class="card animate-fade-slide">
        <h2>View by Region</h2>
        <p>Get a regional overview of elevator statuses on an interactive map.</p>
      </router-link>
      <router-link to="/personal" class="card animate-fade-slide">
        <h2>Personal Center</h2>
        <p>Manage your profile and system settings.</p>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeView'
};
</script>

<style>
.home {
  text-align: center;
  padding: 2rem;
}

.title {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: 1rem;
}

.intro {
  font-size: 1.2rem;
  margin-bottom: 2rem;
}

.card-container {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
}

.card {
  width: calc(25% - 2rem);
  margin: 1rem;
  padding: 1.5rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #f9f9f9;
  text-decoration: none;
  color: #333;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
}

.card h2 {
  color: #007bff;
  margin-bottom: 0.5rem;
}

.card p {
  font-size: 1rem;
}

.animate-fade-slide {
  animation: fadeSlideIn 1s ease both;
}

@keyframes fadeSlideIn {
  0% {
    opacity: 0;
    transform: translateY(20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 1200px) {
  .card {
    width: calc(33.333% - 2rem);
  }
}

@media (max-width: 768px) {
  .card {
    width: calc(50% - 2rem);
  }
}

@media (max-width: 480px) {
  .card {
    width: calc(100% - 2rem);
  }
}
</style>
