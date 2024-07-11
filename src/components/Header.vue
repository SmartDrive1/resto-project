<template>
    <div class="nav">
        <router-link to="/">Home</router-link>
        <router-link to="/addresto">Add Restaurant</router-link>
        <!--<router-link to="updateresto">Update Restaurant</router-link>-->
        <a v-on:click="logout" href="#">Logout</a>

    </div>
</template>

<script>
export default{
    name:'MainHeader',
    methods:{
        logout(){
            localStorage.clear();
            this.$router.push({name:'Login'})
        }
    }
}
</script>

<style>
.nav{
    background-color: skyblue;
    overflow: hidden;
}

.nav a{
    text-decoration: none;
    color: black;
    float: left;
    padding: 14px;
    text-align: center;
    font-size: 17px;
    margin-right: 5px;
    font-weight: 500;
}

.nav a:hover{
    background-color: #0056b3;
    color: white;
}
</style>