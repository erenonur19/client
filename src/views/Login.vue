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
  <form class="box" >
  <div class="field">
    <label class="label">Username</label>
    <div class="control">
      <input class="input" type="text" placeholder="Username">
    </div>
  </div>

  <div class="field">
    <label class="label">Password</label>
    <div class="control">
      <input class="input" type="password" placeholder="********">
    </div>
  </div>
   <br>
   <div class="field">
  <button class="button is-black">Sign in</button>&nbsp;&nbsp;&nbsp;
  
  <button @click="getRegister()" class="button is-danger">Register</button>
   </div>
</form>

</div>

</template>

<script>
import {useRouter} from 'vue-router'
export default {
    setup(){
    const router=useRouter()
      function getRegister(){
          router.push({
            name:'Register',
        
          })
          
        } 
        return{
            getRegister
        }
    }
}
</script>

<style>

</style>