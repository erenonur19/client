<template>
<PostForm :post="post" :submitPost="createPost" />
 
</template>

<script>
import PostForm from '../components/PostForm.vue'
import{reactive} from 'vue'
import{useRouter} from 'vue-router'
import {onMounted} from 'vue'

export default {
components:{
    PostForm
  },

  setup(){
    onMounted(()=>{
            validation()
          
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