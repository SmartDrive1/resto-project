<template>
    <MainHeader />
    <h1> Hello {{ username }}, Welcome on Home Page</h1>
    <table class="restoTB" border="1px">
        <tr>
            <!-- <td>
                ID
            </td> -->
            <td>
                Name
            </td>
            <td>
                Address
            </td>
            <td>
                Contact
            </td>
            <td>
                Actions
            </td>
        </tr>
        <tr v-for="item in restaurant" :key="item.id">
            <!-- <td>
                {{ item.id }}
            </td> -->
            <td>
                {{ item.name }}
            </td>
            <td>
                {{ item.address }}
            </td>
            <td>
                {{ item.contact }}
            </td>
            <td>
                <router-link :to="'/updateresto/' + item.id" class="button">Update</router-link>
                <button v-on:click="deleteResto(item.id, item.name)" class="button">Delete</button>
            </td>
        </tr>
    </table>
</template>

<script>
import MainHeader from './Header.vue'
import axios from 'axios'
export default {
    name: 'HomePage',
    data() {
        return {
            username: '',
            restaurant: []
        }
    },
    components: {
        MainHeader
    },

    methods: {
        async deleteResto(id, name) {
            if (confirm("Do you really want to delete " + name + "?")) {
                console.log('Attempting to delete restaurant with ID:', id); // Log ID being deleted
                try {
                    let result = await axios.delete("http://localhost:3000/restaurants/" + id);
                    if (result.status === 200) {
                        console.log('Deletion successful'); // Log success
                        this.loadData();
                    } else {
                        console.warn('Failed to delete restaurant:', result.status); // Log failure status
                    }
                } catch (error) {
                    console.error('Error deleting restaurant:', error);
                }
            }
        },

        async loadData() {
            let user = localStorage.getItem('user-info')
            this.username = JSON.parse(user).name
            if (!user) {
                this.$router.push({ name: 'SignUp' })
            }
            let result = await axios.get("http://localhost:3000/restaurants");
            //console.warn(result)
            this.restaurant = result.data
        }
    },

    async mounted() {
        this.loadData()
    }
}
</script>

<style>
td {
    width: 160px;
    height: 40px;
}

.restoTB {
    margin-left: auto;
    margin-right: auto;
}

.action-button {
    width: 300px;
    height: 40px;
    background-color: skyblue;
    color: white;
    cursor: pointer;
    border-radius: 4px;
    transition: background-color 0.3s ease;
    text-decoration: none;
    display: inline-block;
    text-align: center;
    line-height: 40px;
    font-size: 15px;
    padding: 0;
    margin: 0;
}

.action-button:hover{
    background-color: #0056b3;
}
</style>