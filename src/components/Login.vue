<template>
  <img src="../assets/logo.jpg" class="logo" alt="" />
  <h1>Login to RMS</h1>
  <div class="login">
    <input type="text" v-model="email" placeholder="enter email ID" />
    <input type="password" v-model="password" placeholder="enter password" />
    <button v-on:click="login">Login</button>
    <p style="margin-top: 100px; text-decoration: none">
      <router-link to="/sign-up">sign up</router-link>
    </p>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      let result = await axios.get(
        `http://localhost:3000/users?email=${this.email}&password=${this.password}`
      );
      if (result.status == 200 && result.data.length > 0) {
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "Home" });
      } else {
        this.email = "";
        this.password = "";
        alert("ID or Password Not Matched");
      }
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (user) {
      this.$router.push({ name: "Home" });
    }
  },
};
</script>
