<template>
  <post-form :post="post" :createPost="updatePost"></post-form>
</template>

<script>
import PostForm from '../components/PostForm.vue'
import {useRouter,useRoute} from 'vue-router'
import {ref, onMounted } from 'vue'



export default {
    components: {
        PostForm,
    },
    setup(){
        const router=useRouter()
        const route=useRoute()
        const API_URL='http://localhost:3000/posts'

        const post=ref({

            userName:'',
            title:'',
            message:''


        })
        onMounted(()=>{
            getPost()
        })

        async function getPost(){
            const{id}=route.params
            const response=await fetch(`${API_URL}/${id}`)
            const json=await response.json()
            post.value=json

        }
        async function updatePost(){
            const{id}=route.params
            const response=await fetch(`${API_URL}/${id}`,{
                method:'PUT',
                headers:{
                    'content-type': 'application-json',
                },
                body: JSON.stringify({
                    userName:post.value.userName,
                    title:post.value.title,
                    message:post.value.message,
                    
                })
            })
            const json=await response.json()
            router.push({
                name:'Home'
            })
        }
        return{
            post,
            updatePost
        }



    }

}
</script>

<style>

</style>