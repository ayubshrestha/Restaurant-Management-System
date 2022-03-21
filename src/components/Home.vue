<template>
  <Header/>
  <h1>Hello {{name}}, you are on Home page</h1>
  <table>
    <thead>
      <tr>
      <th>SN</th>
      <th>Name</th>
      <th>Address</th>
      <th>Contact</th>
      <th>Action</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in restaurants" :key="item.id">
      <td>{{item.id}}</td>
      <td>{{item.name}}</td>
      <td>{{item.address}}</td>
      <td>{{item.contact}}</td>
      <td><router-link :to= "'/update-restaurant/'+item.id">Update</router-link></td>
      </tr>
    </tbody>
  </table>
</template>
<script>
import axios from 'axios'
import Header from './Header.vue'
export default {
  name: "Home",
  data() {
    return({
      name: '',
      restaurants: [],
    })
  },
  components: {
    Header
  },
  async mounted() {
    let user = localStorage.getItem("user-info");
    console.log(user)
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
    this.name = JSON.parse(user).name
    let result = await axios.get("http://localhost:3000/restaurants")
    console.log(result);
    this.restaurants = result.data
  },
};
</script>
<style scoped>
table {
  margin-left: auto;
  margin-right: auto;
  border-collapse: collapse;
}

th, td {
  border: 1px solid lightgray;
  padding-top: 12px;
  padding-bottom: 12px;
  padding-left: 20px;
  padding-right: 20px;
}
tbody tr:nth-child(even) td {
  background-color: #eee;
}

a {
  display: block;
  background-color: transparent !important;
  padding: 0;
  letter-spacing: 0;
  font-size: 16px;
  color: blueviolet;
}

</style>
