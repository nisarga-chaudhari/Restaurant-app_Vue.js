<template>
  <Header v-bind:name=this.uname />
  <h1>Restaurants List</h1>
  <table border="1px">
    <tr>
      <td>Id</td>
      <td>Name</td>
      <td>Contact</td>
      <td>Address</td>
      <td>Action</td>
    </tr>
    <tr v-for="item in restaurant" :key="item.id">
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.contact }}</td>
      <td>{{ item.address }}</td>
      <td>
        <router-link :to="'/update/' + item.id" class="update">Update</router-link>
        <button class="delete-btn" v-on:click="deleteRes(item.id)">delete</button>
      </td>
    </tr>
  </table><br>
  <button class="about" v-on:click="display()">About Us</button>
  <p v-if="show">&Lorem ipsum dolor sit, amet consectetur adipisicing elit. Animi dolor voluptate ullam, fugit, aspernatur assumenda nostrum, ut et in deleniti itaque magnam odio. Tenetur similique excepturi consequatur? Id, voluptate quia.</p>
</template>
 
<script>
import axios from "axios";
import Header from "./Header.vue";
export default {
  name: "Home",
  data() {
    return {
      uname: "",
      restaurant: [],
      show:false,
    };
  },
  components: {
    Header,
  },
  methods: {
    display(){
        this.show = !this.show
    },
    async deleteRes(id) {
      let result = await axios.delete("http://localhost:3000/restaurant/"+id);
      if (result.status == 200) {
        this.loadPage()
      }
    },
    async loadPage() {
      let user = localStorage.getItem("user-info");
      if (!user) {
        this.$router.push({name: 'Login'});
      }
      this.uname = JSON.parse(user)[0].name;
      let result = await axios.get("http://localhost:3000/restaurant");
      this.restaurant = result.data;
    },
  },
  mounted() {
   this.loadPage()
  },
};
</script>
<style>
table {
  margin-left: auto;
  margin-right: auto;
}
td {
  width: 160px;
  height: 40px;
}
.about{
    width: 320px;
    height: 40px;
    border: none;
    background: skyblue;
    color: white;
    cursor: pointer;
}
.about:hover{
    background-color: rgb(92, 180, 215);
}
p{
    padding-left: 10%;
    padding-right: 10%;
}
.delete-btn{
  background-color: rgb(254, 222, 222);
  border: none;
  padding: 5px 10px;
  margin: 10px;
  border-radius: 5px;
}
.delete-btn:hover{
  background-color: rgb(242, 87, 87);
  color: white;
}
.update{
    text-decoration: none;
    color: rgb(5, 155, 20);
    padding: 10px;
}
.update:hover{
    color:rgb(4, 107, 4);
}

</style>

