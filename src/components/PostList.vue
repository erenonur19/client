<template>

  <div class="container">
   <!-- <Modal v-if="!isLoggedIn"/> -->
      <div v-for="post in posts" :key="post._id" class="card my-4">
      <div class="card-content">
    <div class="media">
      <div class="media-content">
        <p><a style="color:blue;"  @click="getirPost(post._id)" class="title is-4">{{post.title}}</a> </p>
      </div>
    </div>
    

    <div class="content">
      {{post.message}}
      <br>
      <strong>Author: {{post.userName}}</strong><br>
      <strong>{{convertDate(post.createdAt)}}</strong>
    </div>

    
    <!-- <button @click="getirPost(post._id)" class="button is-black">Details</button> -->
  
    <!-- <button @click="removePost(post._id)" class="button is-danger ">Delete</button> -->
     
                     
    
     
    
             


    
  </div>
  
</div>  


  </div>
  


</template>

<script>
import { ref,onMounted } from 'vue'
import {useRouter} from 'vue-router'
import Modal from '../components/Modal.vue'


export default {
  components: { Modal },
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
           })
           }
        
        
        }
        
        const router=useRouter()
        const posts=ref([])
        const API_URL='http://localhost:3000/posts'
        onMounted(()=>{
            validation()
            getPosts()     
        })
       function convertDate(date){
         
         var day=date.slice(0,10)
         
         var time=date.slice(11,16)
         
         return "Date: "+day+" Time: "+time;
        }

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
            validation,
            convertDate,
            
        }
    }
}

</script>

<style lang="scss">
.container {
	font-family:Helvetica, Arial;
	text-align: center;
	color: #2c3e50;
  font-size: 150%;

}
</style>