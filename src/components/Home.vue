<template>
  <Header />
  <h1>Hello {{ name }}, you are on Home page</h1>
  <table class="css-serial">
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
        <!-- <td v-for="num in this.restaurants.length" :key="num">{{ num }}</td> -->
        <td>&nbsp;</td>
        <td>{{ item.name }}</td>
        <td>{{ item.address }}</td>
        <td>{{ item.contact }}</td>
        <td style="display: flex">
          <router-link :to="'/update-restaurant/' + item.id">
          Update
          </router-link>
          <button v-on:click="removeResto(item.id)" style="margin-left: 20px">
            X
          </button>
        </td>
      </tr>
    </tbody>
  </table>
</template>
<script>
import axios from "axios";
import Header from "./Header.vue";
export default {
  name: "Home",
  data() {
    return {
      name: "",
      restaurants: [],
      num: ''
    };
  },
  components: {
    Header,
  },
  methods: {
    async removeResto(id) {
      let result = await axios.delete(
        "http://localhost:3000/restaurants/"+id
      );
      console.log(result);
      if (result.status === 200) {
        this.loadData();
      }
    },

    async loadData() {
      let user = localStorage.getItem("user-info");
      if (!user) {
        this.$router.push({ name: "SignUp" });
      }
      this.name = JSON.parse(user).name;
      let result = await axios.get("http://localhost:3000/restaurants");
      this.restaurants = result.data;
    },
  },
  async mounted() {
    this.loadData();
  },
};
</script>
<style scoped>
table {
  margin-left: auto;
  margin-right: auto;
  border-collapse: collapse;
}

th,
td {
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
.css-serial {
 counter-reset: serial-number; /* Set the serial number counter to 0 */
}
.css-serial td:first-child:before {
 counter-increment: serial-number; /* Increment the serial number counter */
 content: counter(serial-number); /* Display the counter */
}
</style>
