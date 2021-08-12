<template>
<div class="container">
    <br>
   <form @submit.prevent="createUser"> 
  <div class="field">
  <label class="label">Name</label>
  <div class="control">
    <input class="input" type="text" v-model="name" placeholder="Name" required>
  </div>
</div>

<div class="field">
  <label class="label">Username</label>
    <input class="input is-success" type="text" placeholder="Username" v-model="userName" required>
  <!-- <p class="help is-success">This username is available</p> -->
</div>

<div class="field">
  <label class="label">Email</label>
    <input class="input is-danger" type="email" placeholder="example@gmail.com" v-model="email" required>
  <!-- <p class="help is-danger">This email is invalid</p> -->
</div>
 <div class="field">
  <label class="label">Password</label>
  <div class="control">
    <input class="input" type="password" placeholder="********" v-model="password" required>
  </div>
</div>
<br>


<div class="field is-grouped">
  <div class="control">
    <button class="button is-black">Register</button>
  </div>
  <div class="control">
    <button class="button is-danger">Cancel</button>
  </div>
</div>
</form>
</div>
</template>

<script>

import axios from 'axios';

export default {

  data(){
  return{
    name:'',
    userName:'',
    email:'',
    password:'',
  }
},
methods:{
  createUser(){
    const newUser={
      name:this.name,
      userName:this.userName,
      email:this.email,
      password:this.password
    }
    axios.post('http://localhost:3000/auth/register',newUser)
    
  }

}

}

</script>

<style>

</style>