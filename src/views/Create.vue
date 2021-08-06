<template>
<PostForm :post="post" :createPost="createPost" />
 
</template>

<script>
import PostForm from '../components/PostForm.vue'
import{reactive} from 'vue'
import{useRouter} from 'vue-router'

export default {
  components:{
    PostForm
  },

  setup(){
    const API_URL='http://localhost:3000/posts'
    const router=useRouter()
    const post=reactive({
      userName:'',
      title:'',
      message:''

    })
    async function createPost(){
      const response=await fetch(API_URL,{
        method:'POST',
        headers:{
          'content-type':'application/json'
        },
        body: JSON.stringify({
          userName:post.userName,
          title:post.title,
          message:post.message

        })
      })
      const result=await response.json()
      router.push({
        name:'Home'
      })

    
    

  }
  return{
    post,
    createPost,
    
  }
}
}
</script>

<style>

</style>