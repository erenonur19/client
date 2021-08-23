<template>
  <PostForm :post="post" :submitPost="updatePost" />
</template>

<script>
import PostForm from '../components/PostForm.vue'
import {ref,reactive,onMounted} from 'vue'
import {useRouter,useRoute} from 'vue-router'
import axios from 'axios'
export default {
components:{
    PostForm
},
setup(){
 const router=useRouter();
 const route=useRoute();
 const API_URL='http://localhost:3000/posts'
const post = ref({
      title: '',
      message:'',
    })
 onMounted(()=>{
     getPost()
 })
  
async function getPost() {
      const { id } = route.params
      const response = await fetch(`${API_URL}/${id}`)
      const json = await response.json()
      post.value = json
    }
    async function updatePost() {
      try {
        const { id } = route.params
        const response = await fetch(`${API_URL}/${id}`, {
          method: 'PUT',
          headers: {
            'content-type': 'application/json',
            token:localStorage.getItem('token')
          },
          body: JSON.stringify({
            title: post.value.title,
            message:post.value.message,
          }),
        })
        const json = await response.json()
        router.push({
          name: 'Posts',
        })
      } catch (err) {
        console.log(err)
      }
    }
return{
    post,
    updatePost,
}


}
}
</script>

<style>

</style>