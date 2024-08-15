<template>
  <div class="register-container">
    <div class="register-form">
      <h2>Welcome</h2>
      <form @submit.prevent="register">
        <div class="input-container">
          <input
            type="text"
            v-model="username"
            placeholder="Username"
            required
          />
          <div class="underline"></div>
        </div>
        <div class="input-container">
          <input type="email" v-model="email" placeholder="Email" required />
          <div class="underline"></div>
        </div>
        <div class="input-container">
          <input
            type="password"
            v-model="password"
            placeholder="Password"
            required
          />
          <div class="underline"></div>
        </div>
        <button type="submit" class="register-btn">Register</button>
        <p v-if="message" class="error-message">{{ message }}</p>
      </form>
      <p>Already have an account? <a href="/">Login</a></p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      username: "",
      email: "",
      password: "",
      message: "",
    };
  },
  methods: {
    async register() {
      if (!this.username || !this.email || !this.password) {
        this.message = "All fields are required";
        return;
      }
      try {
        const response = await axios.post("http://localhost:8082/register", {
          username: this.username,
          email: this.email,
          password: this.password,
        });
        this.message = "Registration successful!";
      } catch (error) {
        this.message = "Registration failed: " + error.response.data;
      }
    },
  },
};
</script>

<style scoped>
.register-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: #f5f5f5;
}

.register-form {
  background: white;
  padding: 40px;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  width: 300px;
  text-align: center;
}

.input-container {
  position: relative;
  margin-bottom: 20px;
}

input {
  width: 100%;
  padding: 10px 5px;
  border: none;
  border-bottom: 2px solid #ccc;
  outline: none;
  transition: border-color 0.3s;
}

input:focus {
  border-bottom-color: #4caf50;
}

.underline {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background-color: #4caf50;
  transition: width 0.3s;
}

input:focus + .underline {
  width: 100%;
}

.register-btn {
  width: 100%;
  padding: 10px;
  border: none;
  background-color: #4caf50;
  color: white;
  border-radius: 20px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.register-btn:hover {
  background-color: #3e8e41;
}

.error-message {
  color: red;
  margin-top: 20px;
}
</style>
