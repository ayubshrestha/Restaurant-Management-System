<template>
  <h1>Hello, You are on Home page</h1>
</template>
<script>
export default {
  name: "Home",
  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>
