<template>
    <Header v-bind:name=this.uname />
    <h1>Update Restaurant Here</h1>
    <form class="form">
        <input type="text" name="name" placeholder="Restaurant Name" v-model="restaurant.name"/>
        <input type="text" name="contact" placeholder="Contact Number" v-model="restaurant.contact"/>
        <input type="text" name="address" placeholder="Restaurant Address" v-model="restaurant.address"/>
        <button v-on:click="updateRestaurant()" type="button">Update Reastaurant</button>
    </form>
</template>

<script>
import axios from 'axios'
import Header from './Header.vue'
export default {
    name: 'Update',
    components:{
        Header
    },
    data(){
        return{
           restaurant:{
            name:'',
            contact:'',
            address:''
           } ,
           uname:'',
        }
    },
    methods:{
        async updateRestaurant(){
            const result=await axios.put('http://localhost:3000/restaurant/'+this.$route.params.id,{
                name:this.restaurant.name,
                contact:this.restaurant.contact,
                address:this.restaurant.address
            });
            if(result.status==200)
            {
                this.$router.push({name:'Home'})
            }
        }
    },
    async mounted(){
        let user = localStorage.getItem('user-info');
        this.uname = JSON.parse(user)[0].name;
        if(!user){
            this.$router.push({name: 'SignUp'})
        }
        const result = await axios.get('http://localhost:3000/restaurant/'+this.$route.params.id)
        this.restaurant=result.data
        //console.log(result.data)
    }
}
</script>