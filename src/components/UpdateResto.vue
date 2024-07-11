<template>
    <MainHeader />
    <h1> Hello {{ username }}, Welcome on Update Restaurant</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Enter Restaurant Name" v-model="restaurant.name">
        <input type="text" name="address" placeholder="Enter Address" v-model="restaurant.address">
        <input type="text" name="contact" placeholder="Enter Contact" v-model="restaurant.contact">
        <button type="button" v-on:click="updateResto" class="button-link">Update Restaurant</button>
    </form>
</template>

<script>
import MainHeader from './Header.vue'
import axios from 'axios'
export default {
    name: 'UpdateResto',

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

    components: {
        MainHeader
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

        async updateResto() {
            if (this.validate()) {
                const result = await axios.put("http://localhost:3000/restaurants/" + this.$route.params.id, {
                    name: this.restaurant.name,
                    address: this.restaurant.address,
                    contact: this.restaurant.contact
                });

                if (result.status == 200) {
                    this.$router.push({ name: 'Home' })
                }

                console.warn("result", result)
            } else {
                return
            }
        }
    },

    async mounted() {
        let user = localStorage.getItem('user-info')
        this.username = JSON.parse(user).name
        if (!user) {
            this.$router.push({ name: 'SignUp' })
        }

        const result = await axios.get('http://localhost:3000/restaurants/' + this.$route.params.id)
        // console.warn(result.data)
        this.restaurant = result.data
    }
}
</script>