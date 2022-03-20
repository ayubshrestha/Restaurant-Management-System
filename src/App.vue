<template>
  <router-view/>
</template>

<script>

export default {
  name: 'App',
}
</script>

<style>
#app {
 
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body{
    font-family: 'Open Sans', sans-serif;
}

.logo {
  height: 150px;
  width: 250px;
}

/* .register {
    border: 1px solid skyblue;
    padding-top: 50px;
    margin-right: auto;
    margin-left: auto;
    border-radius: 6px;
    padding-bottom: 50px;
    width: 500px;
    background-color: rgb(174, 248, 171);
} */
.register input, .login input {
  display: block;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 30px;
  height: 32px;
  width: 300px;
  padding: 8px;
  padding-left: 30px !important;
  border: 1px solid skyblue;
  border-radius: 20px;
  box-shadow: rgb(0 0 0 / 24%) 0px 3px 8px;
}
::-webkit-input-placeholder {
  color: rgb(23, 150, 201);
}

.register button, .login button {
  width: 320px;
  height: 40px;
  border: 1px solid skyblue;
  color: #fff;
  background-color: skyblue;
  border-radius: 20px;
  cursor: pointer;
}
a:-webkit-any-link {
    color: skyblue;
    cursor: pointer;
    text-decoration: none;
    font-weight: 600;
    letter-spacing: 0.3ex;
    font-size: 20px;
    background-color: #2c3e50;
    padding: 20px;
    border-radius: 10px;
}
a:-webkit-any-link:hover {
    opacity: 0.8;
}

</style>
