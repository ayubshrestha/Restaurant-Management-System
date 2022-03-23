<template>
    <Header/>
    <h1>Hello {{name}}, you can update restaurants here</h1>
    <form class="form">
        <h2>Please fill the form to update</h2>
        <label for="name">Edit Restaurant Name:</label>
        <input type="text"  name="name" v-model="restaurants.name">
        <label for="address">Edit Address</label>
        <input type="text" name="address" v-model="restaurants.address" >
        <label for="contact">Edit Contact</label>
        <input type="number" name="contact" v-model="restaurants.contact">
        <button type="button" v-on:click="updateResto">Update</button>
    </form>
</template>
<script>
    import axios from 'axios'
    import Header from './Header.vue'
    export default {
        name: 'Update',
        data() {
            return ({
                name: '',
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
        methods: {
            async updateResto() {
                let result = await axios.put("http://localhost:3000/restaurants/" + this.$route.params.id, {
                    name: this.restaurants.name,
                    address: this.restaurants.address,
                    contact: this.restaurants.contact
                })
                if(result.status == 200){
                    this.$router.push({name:'Home'})
                }
        
                
            }
        },
        async mounted() {
            let user = localStorage.getItem("user-info");
            if(!user){
                this.$router.push({name: 'SignUp'})
            }

            console.log(this.$route.params.id)
            let result = await axios.get("http://localhost:3000/restaurants/" + this.$route.params.id)
            this.restaurants = result.data
            console.log(result)
        }

    }
</script>

<style scoped>
    input {
        color: gray;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    }
</style>