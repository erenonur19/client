<template>
<div class="container">
     <br>
     
     
 
 <form @submit.prevent="createPost">
   <!-- <div class="field">
  <label class="label">Username</label>
  <div class="control">
    <input v-model="post.userName" class="input" type="text" placeholder="Text input" required>
  </div>
</div> -->

<div class="field">
  <label class="label">Title</label>
  <div class="control">
    <input v-model="post.title" class="input" type="text" placeholder="Text input" required>
  </div>
</div>


<div class="field">
  <label class="label">Message</label>
  <div class="control">
    <textarea v-model="post.message" class="textarea" placeholder="Textarea" required></textarea>
  </div>
</div>


<div class="field is-grouped">
  <div class="control">
    <button type="submit" class="button is-black">Submit</button>
  </div>
  <div class="control">
    <button class="button is-danger">Cancel</button>
  </div> 
</div></form>


 </div>
 
</template>

<script>

import{reactive} from 'vue'
import{useRouter} from 'vue-router'
import {onMounted} from 'vue'

export default {


  setup(){
    onMounted(()=>{
            //validation()
          
        })
    const API_URL='http://localhost:3000/posts'
    const router=useRouter()
    function validation(){
          if(localStorage.getItem('token')===null){
            alert('You need to be logged in before you access the content..')
          router.push({
            name:'Login',
          })}
        
        }
    const post=reactive({
      title:'',
      message:''

    })
    async function createPost(){
      const response=await fetch(API_URL,{
        method:'POST',
        headers:{
          'content-type':'application/json',
           token:localStorage.getItem('token')
        },
        body: JSON.stringify({
          userName:post.userName,
          title:post.title,
          message:post.message

        })
      })
      const result=await response.json()
      router.push({
        name:'Posts'
      })

    
    

  }
  return{
    post,
    createPost,
    validation,
    
  }
}
}
</script>

<style>

</style>