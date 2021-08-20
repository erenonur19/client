<template>

  <div class="container">
    
      <div v-for="post in posts" :key="post._id" class="card my-4">
      <div class="card-content">
    <div class="media">
      <div class="media-content">
        <p><a @click="getirPost(post._id)" class="title is-4">{{post.title}}</a> </p>
      </div>
    </div>
    

    <div class="content">
      {{post.message}}
      <br>
      <strong>Author: {{post.userName}}</strong>
    </div>

    
    <button @click="getirPost(post._id)" class="button is-black">Details</button>
  
    <button @click="removePost(post._id)" class="button is-danger ">Delete</button>
     
                     
    
     
    
             


    
  </div>
  
</div>  


  </div>
  


</template>

<script>
import { ref,onMounted } from 'vue'
import {useRouter} from 'vue-router'
export default {
  created(){
    if (localStorage.getItem('reloaded')) {
       
        localStorage.removeItem('reloaded');
    } else {
        
        localStorage.setItem('reloaded', '1');
        location.reload();
    }
  },
    setup(){
      function validation(){
          if(localStorage.getItem('token')===null){
            alert('You need to be logged in before you access the content..')
          router.push({
            name:'Login',
          })}
        
        }
        
        const router=useRouter()
        const posts=ref([])
        const API_URL='http://localhost:3000/posts'
        onMounted(()=>{
            
            validation()
            getPosts()
           
            
        
        })

        async function getPosts(){
                
                const response=await fetch(API_URL,{headers: {token:localStorage.getItem('token')}})
                const json=await response.json()
                posts.value=json;
                 
            
        }
        async function removePost(_id){
             const respone=await fetch(`${API_URL}/${_id}`,{
               method:'DELETE',
             })
             getPosts()
             
        }
        async function editPost(_id){
          router.push({
            name:'Update',
            params:{
              id:_id,
            },
          })
          
        } 
        async function getirPost(_id){
          router.push({
            name:'Post',
            params:{
              id:_id,
            },
          })
          
        } 
        return{
            posts,
            removePost,
            editPost,
            getirPost,
            validation
        }
    }
}

</script>

<style>

</style>