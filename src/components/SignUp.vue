<template>
  <img src="../assets/logo.jpg" class="logo" alt="" />
  <h1>Sign Up for RMS</h1>
  <div class="register">
    <input type="text" v-model="name" placeholder="enter name" />
    <input type="text" v-model="email" placeholder="enter email ID" />
    <input type="password" v-model="password" placeholder="enter password" />
    <button v-on:click="signUp">Sign Up</button>
    <p style="margin-top: 100px">
      <router-link to="/login">login</router-link>
    </p>
  </div>
</template>  
<script>
import axios from "axios";
export default {
  name: "Signup",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async signUp() {
      console.log("Sign UP", this.name, this.email, this.password);
      let result = await axios.post("http://localhost:3000/users", {
        name: this.name,
        email: this.email,
        password: this.password,
      });
      console.log(result);
      if (result.status == 201) {
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "Home" });
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
<style></style>
