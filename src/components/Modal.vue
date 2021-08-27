<template>
   <div v-if="isLoggedIn" class="modal is-active">
  <div class="modal-background"></div>
  <div class="modal-content">
    <div class="box">
      <h1>You need to be logged in before you access the content..</h1>
    </div>
    <button @click="goLogin">Login</button>
    <button @click="goRegister">Register</button>
  </div>
  
</div>
</template>

<script>
export default {
   data: () => {
      return {
        isLoggedIn:false
      }
    },
    mounted() {
     if(localStorage.getItem('token')===null){
            this.isLoggedIn=false;
            
           }
          else{
            this.isLoggedIn=true;
          }
    },
methods:{
      goLogin(){
 this.$router.push({
    name:'Login'
  })
      },
      goRegister(){
 this.$router.push({
    name:'Register'
  })
      },

    
},

}
</script>

<style>

</style>