<template>
    <div class="navbar">
        <ul>
            <router-link to= "/" >Home</router-link>
            <router-link to="add-restaurant">Add Restaurant</router-link>
            <!-- <router-link to="update-restaurant">Update Restaurant</router-link> -->
            <a href="#" v-on:click="logout">Logout</a>
        </ul>
    </div>
</template>
<script>
    export default {
        name: 'Header',
        methods: {
            logout(){
                localStorage.clear();
                this.$router.push({name: 'Login'})
            }
        }
    }
</script>

<style scoped>
    .navbar {
        margin-bottom: 30px;
    }

    .navbar ul a {
        border-radius: 0 !important;
    }
</style>
