<template>

<div class="container">
  <PageLoader />
  <div class="card">
  <div class="card-image">
    <figure style="text-align:center">
      <img src="https://envercolakoglu.com/wp-content/uploads/2020/02/forum.png" alt="Placeholder image">
    </figure>
    
  </div>
  <div class="car my-4">
  <div class="card-content">
    <div class="media">
      <div class="media-content">
        <p class="title is-4">Title:{{post.title}}</p>
        <p class="subtitle is-6">@{{post.userName}}</p>
      </div>
    </div>
     <div class="content">
      {{post.message}}
  </div>
<div class="content">
      {{convertDate(post.createdAt)}}
  </div>
 
      
    </div>
  </div>
  <div v-for="message in messages" :key="message._id" class="card my-4">
   <article class="media">
  <figure class="image is-64x64">
  <img class="is-rounded" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTTOkHm3_mPQ5PPRvGtU6Si7FJg8DVDtZ47rw&usqp=CAU">
</figure>
  <div class="media-content">
    <div class="content">
       
        <strong style="color:blue;">&nbsp;&nbsp;{{message.userName}}</strong> <small>{{convertDate(message.createdAt)}}</small>
        <br>
       &nbsp;&nbsp;&nbsp; {{message.message}}
      
    </div>
    <nav class="level is-mobile">
      <div class="level-left">
        <a class="level-item">
          <span class="icon is-small"><i class="fas fa-reply"></i></span>
        </a>
        <a class="level-item">
          <span class="icon is-small"><i class="fas fa-retweet"></i></span>
        </a>
        <a class="level-item">
          <span class="icon is-small"><i class="fas fa-heart"></i></span>
        </a>
      </div>
    </nav>
  </div>
 
</article>
</div>
</div>

<form @submit.prevent="postMessage" class="submitForm"> 
 <article class="media">
  <figure class="media-left">
    <p class="image is-64x64">
      <img class="is-rounded" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTTOkHm3_mPQ5PPRvGtU6Si7FJg8DVDtZ47rw&usqp=CAU">
    </p>
  </figure>
  <div class="media-content">
    <div class="field">
      <!-- <label class="label">Username</label>
      
  <div class="control">
    <input v-model="newMessage.userName" class="input" type="text" placeholder="Text input" required>
  </div>
   -->
  <!-- <label class="label">Title</label>
  <div class="control">
    <input v-model="newMessage.title" class="input" type="text" placeholder="Text input">
  </div> -->
  
  <!-- <label class="label">Message</label> -->
      <p class="control">
        <textarea v-model="newMessage.message" class="textarea" placeholder="Add a comment..." required></textarea>
      </p>
    </div>
    <div class="field">
      <p class="control">
        <button type="submit" class="button is-black btnsb">Post comment</button>
      </p>
    </div>
  </div>
</article> 
</form>

</div>
</template>

<script>
import {useRouter,useRoute} from 'vue-router'
import PageLoader from '../components/PageLoader.vue'


import {ref,reactive, onMounted } from 'vue'
import axios from 'axios'
export default{
 components: {
    PageLoader
  },
  
  
setup(){
    const route=useRoute();
    const API_URL='http://localhost:3000/posts'
    const post=ref({
        userName:'',
        title:'',
        message:'',
        createdAt:''
    })
    const messages=ref([])
    const newMessage=reactive({
      message:'',
    })
    function convertDate(date){
         
         var day=date.slice(0,10)
         
         var time=date.slice(11,16)
         
         return day+"/"+time;
        }
    

   if (localStorage.getItem('reloaded')) {
        localStorage.removeItem('reloaded');
    } else {
      setTimeout(() => {
        localStorage.setItem('reloaded', '1');
        location.reload();
      }, 2000);
        
    }
  Promise.all([getPost(),getMessages()])
  

function getPost(_id){
    
    return new Promise((resolve,reject)=>{
    const{id}=route.params
    axios.get(`${API_URL}/${id}`).then(res=>{
    post.value=res.data
    resolve(post)
    }).catch((err)=>{
    reject(err)
    })
    }) 
}
function getMessages(_id){

     return new Promise((resolve,reject)=>{
     const{id}=route.params
     axios.get(`${API_URL}/${id}/comments`).then(res=>{
       messages.value=res.data
       resolve(messages)
     })
     .catch((err)=>{
         reject(err)
     }) 
     })
     
}
async function postMessage(){
     const {id}=route.params
     const response=await fetch(`${API_URL}/${id}/comments`,{
       method:'POST',
       headers:{
         'content-type':'application/json',
         token:localStorage.getItem('token')
       },
       body: JSON.stringify({
        userName:newMessage.userName,
        message:newMessage.message,
        title:newMessage.title

       })
     })
      const res=await response.json();
      location.reload();
      
      
  

}
return{
    post,
    messages,
    newMessage,
    getPost,
    getMessages,
    postMessage,
    convertDate,
    
    
    
}

}
}
</script>

<style>
.footer {
    font-size: 15px;
    text-align: center;
    height: 80px;
    padding: 20px;
    
}
  .btnsb
   {
      position:relative;
      left:1100px;
      top:16px

   }
   .submitForm{
     border-style: solid;
     
   }
</style>
