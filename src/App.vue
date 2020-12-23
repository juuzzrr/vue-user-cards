<template>
  <div id="app">
    <UserCard 
    v-bind:nickname="nickname"
    v-bind:photo="photo"
    v-bind:firstname="firstName"
    v-bind:lastname="lastName"
    v-bind:phone="phone"
    v-bind:address="address"
    v-bind:email="email"
    v-bind:city="city"
    />
    <button v-on:click="getUserData">
      Обновить профиль
    </button>
  </div>
</template>

<script>
import UserCard from "./components/UserCard.vue";
export default {
  name: "app",
  components: {
    UserCard
  },
  data() {
    return{
      photo: '',
      firstName: '',
      lastName: '',
      nickname: '',
      city: '',
      address: '',
      email: '',
      phone: '',
    }
  },
  methods:{
    getUserData(){
      this.axios.get("http://37.77.104.246/users/getrandom.php")
      .then( (response)=>{
          this.photo=response.data.img;
          this.firstName=response.data.firstName;
          this.lastName=response.data.lastName;
          this.nickname = response.data.email.split('@')[0];
          this.address=response.data.address;
          this.phone=response.data.phone;
          this.city=response.data.city;
          this.email=response.data.email;
        }
    )
  }
},
mounted(){
  this.getUserData();
}
};
</script>
<style>
</style>