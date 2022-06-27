<template>
    <Header v-bind:name=this.uname />
    <h1>Add Restaurant Here</h1>
    <form class="form">
        <input type="text" name="name" placeholder="Restaurant Name" v-model="restaurant.name"/>
        <input type="text" name="contact" placeholder="Contact Number" v-model="restaurant.contact"/>
        <input type="text" name="address" placeholder="Restaurant Address" v-model="restaurant.address"/>
        <button v-on:click="addRestaurant()" type="button">Add Reastaurant</button>
    </form>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
    name: 'Add',
    components:{
        Header
    },
    data(){
        return{
           restaurant:{
            name:'',
            contact:'',
            address:''
           },
           uname:'' 
        }
    },
    methods:{
        async addRestaurant(){
            const result = await axios.post('http://localhost:3000/restaurant',{
                name:this.restaurant.name,
                contact:this.restaurant.contact,
                address:this.restaurant.address
            })
            if(result.status==201)
            {
                this.$router.push({name:'Home'})
            }
        }
    },
    mounted(){
        let user = localStorage.getItem('user-info');
        this.uname = JSON.parse(user)[0].name;
        if(!user){
            this.$router.push({name: 'SignUp'})
        }
    }
}
</script>