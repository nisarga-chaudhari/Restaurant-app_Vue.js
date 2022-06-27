<template>
    <div class="nav">
        <router-link to="/">Home</router-link>
        <router-link to="/add">Add Restaurant</router-link>
        <router-link v-on:click="logout()" to="/login">Logout</router-link>
        <p class="right">Hi, {{name}}</p>
    </div>
    
</template>
<script>
export default {
    name:'Header',
    props:['name'],
    methods:{
        logout(){
            localStorage.clear();
            this.$router.push({name: 'Login'})
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
    float: left;
    color: black;
    padding: 14px 16px;
    text-align:center;
    font-size: 17px;
    text-decoration: none;
    margin-right: 5px;
}
.nav a:hover{
    
    color:white
}
.right{
    text-align: right;
    padding-right: 30px;
}
</style>