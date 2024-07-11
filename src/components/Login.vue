<template>
    <div class="container">
        <div class="left-side">
            <div class="login">
                <img class="logoEdit" src="../assets/logo.png">
                <h2 id="h2class">Welcome Back!</h2>
                <input type="text" v-model="email" placeholder="Enter Email" />
                <input type="password" v-model="password" placeholder="Enter Password" />
                <button v-on:click="login" class="button">Login</button>
                <p>
                    <router-link to="/sign-up" class="button-link">Sign Up</router-link>
                </p>
            </div>
        </div>
        <div class="right-side">

        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: "LoginPage",
    data() {
        return {
            email: '',
            password: ''
        }
    },
    methods: {
        async login() {
            if (!this.email && !this.password) {
                alert('Email and Password are Required')
                return;
            }

            if (!this.email) {
                alert('Email is Required')
                return;
            }

            if (!this.password) {
                alert('Password is Required')
                return;
            }

            try {
                let response = await axios.get(`http://localhost:3000/user?email=${this.email}`);
                let userData = response.data;

                if (userData.length === 0) {
                    alert('User not found');
                    return;
                }

                if (userData[0].password === this.password) {
                    localStorage.setItem("user-info", JSON.stringify(userData[0]));
                    this.$router.push({ name: 'Home' });
                } else {
                    alert('Email or Password is Incorrect');
                }
            } catch (error) {
                console.error('Error logging in:', error);
            }
        }
    }
}
</script>
.h2class{
    align-items: left;
}
<style>
</style>