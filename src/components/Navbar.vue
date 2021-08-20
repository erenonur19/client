<template>
  <nav class="navbar is-black" role="navigation" aria-label="main navigation">
  <div class="navbar-brand">
    <!-- <a class="navbar-item" href="https://bulma.io">
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSfBtXNjeuwZj7t8ND6RTkfBTTPy1egnIyOPw&usqp=CAU" width="100" height="35">
    </a> 
    <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
    </a>
  
    -->
    

    
  </div>

  <div id="navbarBasicExample" class="navbar-menu">
    <div class="navbar-start">
    <strong class="navbar-item">FORUMAPI</strong>    


    <a class="navbar-item" href="http://localhost:8080/login">
        <strong>Log In</strong>
      </a>

      <a class="navbar-item" href="http://localhost:8080/posts">
        <strong>Posts</strong>
      </a>
      <a class="navbar-item" href="http://localhost:8080/create">
        <strong>New Post</strong>
      </a>
      
      
      
    </div>

    <div class="navbar-item has-dropdown is-hoverable ">
    <a class="navbar-link " >
    <strong >{{user2.userName}}</strong>
  </a>


  <div class="navbar-dropdown">
    <a class="navbar-item" href="http://localhost:8080/profile">
    Profile
  </a>
  <a @click="logOut" class="navbar-item" href="http://localhost:8080/login">
    Log Out
  </a>
  </div>
  
  
</div>

  </div>
</nav>
</template>

<script>
import {onMounted} from 'vue'
import{reactive} from 'vue'
export default {
  
    setup(){
    onMounted(()=>{
    getUserName();
})
const user2=reactive({
      name:'',
      userName:'',

    })
function logOut(){
       localStorage.clear();
       this.$router.push({
         name:'Login'
       })
    }
    async function getUserName(){
  
    const response=await fetch('http://localhost:3000/auth/username',{headers:{token:localStorage.getItem('token')}})
    const json=await response.json()
    
    user2.name=json.name;
    user2.userName=json.userName;
    
    }
    return{
    logOut,
    getUserName,
    user2,
  }  
  },
  
  
    


}
</script>

<style>

</style>