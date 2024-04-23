<template>
  <div class="auth-container">
    <h2>User Authentication</h2>
    <div v-if="errorMessage" class="error-message">{{ errorMessage }}</div>
    <form @submit.prevent="isLogin ? loginUser() : registerUser()">
      <div class="form-group">
        <label for="username">Username:</label>
        <input type="text" id="username" v-model="user.username" required />
      </div>
      <div class="form-group">
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="user.password" required />
      </div>
      <div class="form-group">
        <button type="submit">{{ isLogin ? 'Login' : 'Register' }}</button>
      </div>
      <div class="switch-mode">
        <p>{{ isLogin ? 'Need an account?' : 'Already have an account?' }}
          <a href="#" @click="toggleMode">{{ isLogin ? 'Register' : 'Login' }}</a>
        </p>
      </div>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      user: {
        username: '',
        password: ''
      },
      isLogin: true,
      errorMessage: ''
    };
  },
  methods: {
    toggleMode() {
      this.isLogin = !this.isLogin;
      this.errorMessage = '';
    },
    registerUser() {
      axios.post('http://localhost:8080/api/users/register', this.user)
        .then(response => {
          // Handle success, possibly redirect or clear form
          console.log(response.data);
          this.toggleMode();
        })
        .catch(error => {
          // Handle error, display error message to user
          this.errorMessage = error.response.data.message;
        });
    },
    loginUser() {
      axios.post('http://localhost:8080/api/users/login', this.user)
        .then(response => {
          // Handle success, possibly store token and redirect
          console.log(response.data);
          // Redirect to user profile or dashboard
        })
        .catch(error => {
          // Handle error, display error message to user
          this.errorMessage = error.response.data.message;
        });
    }
  }
};
</script>

<style scoped>
.auth-container {
  max-width: 300px;
  margin: auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.form-group {
  margin-bottom: 15px;
}

.form-group label {
  display: block;
}

.form-group input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.form-group button {
  width: 100%;
  padding: 10px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.form-group button:hover {
  background-color: #0056b3;
}

.error-message {
  color: red;
  margin-bottom: 15px;
}

.switch-mode {
  text-align: center;
}

.switch-mode a {
  color: #007bff;
  text-decoration: none;
}

.switch-mode a:hover {
  text-decoration: underline;
}
</style>
