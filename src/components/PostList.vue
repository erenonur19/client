<template>

  <div class="container">
    
      <div v-for="post in posts" :key="post._id" class="card my-4">
      <div class="card-content">
    <div class="media">
      <div class="media-content">
        <p class="title is-4">{{post.title}}</p> 
      </div>
    </div>
    

    <div class="content">
      {{post.message}}
      <br>
      <strong>Author: {{post.userName}}</strong>
    </div>
    
    <button @click="editPost(post._id)" class="button is-success">Edit</button>
  
    <button @click="removePost(post._id)" class="button is-danger ">Delete</button>
                          
    
     
    
             


    
  </div>
</div>  

  </div>
  


</template>

<script>
import { ref,onMounted } from 'vue'
import {useRouter} from 'vue-router'
export default {
    setup(){
        const router=useRouter()
        const posts=ref([])
        const API_URL='http://localhost:3000/posts'
        onMounted(()=>{
            getPosts()
        })

        async function getPosts(){
                
                const response=await fetch(API_URL)
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
        return{
            posts,
            removePost,
            editPost,
        }
    }
}

</script>

<style>

</style>