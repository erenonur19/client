<template>
<div class="container" >
    <br>
    <br>
    <br>
    <br>
<figure style="text-align:center">
      <img src="https://envercolakoglu.com/wp-content/uploads/2020/02/forum.png" alt="Placeholder image">
      <h1>Join the Community!</h1>
      <br>
      
    </figure>
  <form class="box" @submit.prevent="logIn">
  <div class="field">
    <label class="label" >Username</label>
    <div class="control">
      <input class="input" v-model="username" type="text" placeholder="Username">
    </div>
  </div>

  <div class="field">
    <label class="label">Password</label>
    <div class="control">
      <input class="input" v-model="password" type="password" placeholder="********">
    </div>
  </div>
   <br>
   <div class="field">
  <button type="submit" class="button is-black">Log in</button>&nbsp;&nbsp;&nbsp;
  
  <button @click="getRegister()" class="button is-danger">Register</button>
  <br>
  <br>
  <strong style="color:red;">{{error}}</strong>
   </div>
</form>

</div>

</template>

<script>
import {useRouter} from 'vue-router';
import axios from 'axios'
import {onMounted} from 'vue'
export default {
    
    data(){
      return{
      username:'',
      password:'',
      error:'', 
      
      


      }
    } ,
    methods:{
      goPosts(){
 this.$router.push({
    name:'Posts'
  })
      },
      getRegister(){
 this.$router.push({
    name:'Register'
  })
      },
       

      async logIn(){
        let user={
          username:this.username,
          password:this.password,

        }
        await axios.post('http://localhost:3000/auth/login',user)
        .then(res=>{
          if(res.status=200)
          window.localStorage.setItem('token', res.data.token)
          
          this.$router.push({
            name:'Posts'
          })
          
        }).catch(err=>{
          this.error=err.response.data.error;
        })
          
        
      }
      
    },
  

  

}
</script>

<style>

</style>