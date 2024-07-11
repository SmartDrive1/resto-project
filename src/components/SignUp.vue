<template>
    <div class="container">
        <div class="left-side">
            <div class="register">
                <img class="logoEdit" src="../assets/logo.png">
                <h2>Sign Up</h2>
                <input type="text" v-model="name" placeholder="Enter Name" />
                <input type="text" v-model="email" placeholder="Enter Email" />
                <input type="password" v-model="password" placeholder="Enter Password" />
                <button v-on:click="signUp">Sign Up</button>
                <p>
                    <router-link to="/login" class="button-link">Login</router-link>
                </p>
            </div>
        </div>
        <div class="right-side">

        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'SignUp',
    data() {
        return {
            name: '',
            email: '',
            password: ''
        }
    },
    methods: {
        async signUp() {
            let emailExists = await this.checkEmailExists(this.email)

            if (!this.name) {
                alert('Name cannot be Empty')
                return
            }
            if (!this.email) {
                alert('Email cannot be Empty')
                return
            }
            if (!this.password) {
                alert('Password cannot be Empty')
                return
            }

            if (emailExists) {
                alert('Email already exists')
                return
            }

            let result = await axios.post("http://localhost:3000/user", {
                email: this.email,
                password: this.password,
                name: this.name
            });

            console.warn(result);
            if (result.status == 201) {
                localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push({ name: 'Home' })
            }


        },
        async checkEmailExists(email) {
            try {
                let response = await axios.get(`http://localhost:3000/user?email=${email}`);
                return response.data.length > 0;
            } catch (error) {
                console.error('Error checking email existence:', error);
                return false;
            }
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (user) {
            this.$router.push({ name: 'Home' })
        }
    }
}
</script>