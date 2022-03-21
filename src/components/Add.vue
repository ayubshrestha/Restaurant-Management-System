<template>
    <Header/>
    <h1>Hello {{name}}, you can add restaurants here</h1>
    <form class="form">
        <h2>Please fill the form</h2>
        <label for="name">Restaurant Name:</label>
        <input type="text"  name="name" v-model="restaurants.name">
        <label for="address">Address</label>
        <input type="text" name="address" v-model="restaurants.address" >
        <label for="contact">Contact</label>
        <input type="number" name="contact" v-model="restaurants.contact">
        <button type="button" v-on:click="addResto">Add</button>
    </form>
</template>
<script>
    import axios from 'axios'
    import Header from './Header.vue'
    export default {
        name: 'Add',
        data() {
            return({
                name : '',
                restaurants: {
                    name: '',
                    address: '',
                    contact: ''
                }
            })
        },
        components: {
            Header
        },
        mounted() {
            let user = localStorage.getItem("user-info");
            // this.name = JSON.parse(user).name
            if(!user){
                this.$router.push({name: 'SignUp'})
            }
        },
        methods: {
            async addResto(){
                console.warn(this.restaurants);
                let result = await axios.post("http://localhost:3000/restaurants", {
                    name: this.restaurants.name,
                    address: this.restaurants.address,
                    contact: this.restaurants.contact,
                })
                console.log(result)

                if(result.status == 201) {
                    this.$router.push({name: 'Home'})
                }
            }
        }
    }
</script>
