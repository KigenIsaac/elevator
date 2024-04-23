<template>
    <div class="personal-center">
      <h1>Personal Center</h1>
      <form @submit.prevent="updateProfile">
        <div class="form-group">
          <label for="username">Username</label>
          <input type="text" id="username" v-model="user.username" />
        </div>
        <div class="form-group">
          <label for="email">Email</label>
          <input type="email" id="email" v-model="user.email" />
        </div>
        <!-- Add other profile fields as necessary -->
        <div class="form-group">
          <button type="submit">Update Profile</button>
        </div>
      </form>
      <form @submit.prevent="changePassword">
        <div class="form-group">
          <label for="password">New Password</label>
          <input type="password" id="password" v-model="newPassword" />
        </div>
        <div class="form-group">
          <button type="submit">Change Password</button>
        </div>
      </form>
      <!-- System Preferences can be added here -->
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        user: {
          username: '',
          email: '',
          // Add other profile fields as necessary
        },
        newPassword: ''
      };
    },
    mounted() {
      this.fetchUserProfile();
    },
    methods: {
      fetchUserProfile() {
        axios.get('/api/user/profile') // Replace with your actual endpoint
          .then(response => {
            this.user = response.data;
          })
          .catch(error => {
            console.error('Error fetching user profile:', error);
          });
      },
      updateProfile() {
        axios.put('/api/user/profile', this.user) // Replace with your actual endpoint
          // eslint-disable-next-line no-unused-vars
          .then(response => {
            alert('Profile updated successfully!');
          })
          .catch(error => {
            console.error('Error updating profile:', error);
          });
      },
      changePassword() {
        axios.put('/api/user/change-password', { newPassword: this.newPassword }) // Replace with your actual endpoint
          // eslint-disable-next-line no-unused-vars
          .then(response => {
            alert('Password changed successfully!');
            this.newPassword = '';
          })
          .catch(error => {
            console.error('Error changing password:', error);
          });
      }
    }
  };
  </script>
  
  <style>
  .personal-center {
    max-width: 600px;
    margin: auto;
    padding: 2rem;
  }
  
  .form-group {
    margin-bottom: 1rem;
  }
  
  .form-group label {
    display: block;
    margin-bottom: 0.5rem;
  }
  
  .form-group input,
  .form-group button {
    width: 100%;
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  
  .form-group button {
    background-color: #007bff;
    color: white;
    cursor: pointer;
  }
  
  .form-group button:hover {
    background-color: #0056b3;
  }
  
  @media (max-width: 768px) {
    .personal-center {
      padding: 1rem;
    }
  }
  </style>
  