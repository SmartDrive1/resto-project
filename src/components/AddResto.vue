<template>
    <MainHeader />
    <h1> Hello {{ username }}, Welcome on Add Restaurant</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Enter Restaurant Name" v-model="restaurant.name">
        <input type="text" name="address" placeholder="Enter Address" v-model="restaurant.address">
        <input type="text" name="contact" placeholder="Enter Contact" v-model="restaurant.contact">
        <button type="button" v-on:click="addRestaurant">Add New Restaurant</button>
    </form>
</template>

<script>
import MainHeader from './Header.vue'
import axios from 'axios'
export default {
    name: 'AddResto',

    data() {
        return {
            username: '',
            restaurant: {
                name: '',
                address: '',
                contact: ''
            }
        }
    },

    methods: {

        validate() {
            if (!this.restaurant.name) {
                alert('Restaurant Name cannot be Empty')
                return false
            }
            if (!this.restaurant.address) {
                alert('Address cannot be Empty')
                return false
            }
            if (!this.restaurant.contact) {
                alert('Contact cannot be Empty')
                return false
            }
            return true
        },

        async addRestaurant() {
            if (this.validate()) {
                const result = await axios.post("http://localhost:3000/restaurants", {
                    name: this.restaurant.name,
                    address: this.restaurant.address,
                    contact: this.restaurant.contact
                });

                if (result.status == 201) {
                    this.$router.push({ name: 'Home' })
                }

                console.warn("result", result)
            } else {
                return
            }
        }
    },

    components: {
        MainHeader
    },

    mounted() {
        let user = localStorage.getItem('user-info');
        this.username = JSON.parse(user).name;
        if (!user) {
            this.$router.push({ name: 'SignUp' })
        }
    }
}
</script>