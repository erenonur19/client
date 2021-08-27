<template>
<div class="container">

<div class="container section">
      <div class="card">
  <div class="card-content">
    <div class="media">
      <div class="media-left">
        <figure class="image is-128x128">
          <img src="https://cdn.pixabay.com/photo/2015/10/05/22/37/blank-profile-picture-973460_960_720.png" alt="Placeholder image">
        </figure>
      </div>
      <div class="media-content">
        <p class="title is-2">{{profile.name}}</p>
        <p class="subtitle is-5">@{{profile.username}}</p>
        <p class="subtitle is-8">{{profile.email}}</p>
      </div>
    </div>

    <article class="message is-dark">
  <div class="message-body">
    "My name is Alex Drysdale and I am a Junior Web Developer for Oswald Technologies. I am an accomplished coder and programmer, and I enjoy using my skills to contribute to the exciting technological advances that happen every day at Oswald Tech. I graduated from the California Institute of Technology in 2016 with a Bachelor's Degree in Software Development. While in school, I earned the 2015 Edmund Gains Award for my exemplary academic performance and leadership skills.
  </div>
 
</article>
  </div>
</div>
<br>
<strong>Posts:</strong>
    <br>
  <hr />
     <div v-for="post in posts2" :key="post._id" id="Posts">
       <div class="card">
  <header class="card-header">
    <p class="card-header-title">
     <a href="#" @click="getPost2(post._id)"> {{post.title}} </a>
    </p>
    <button class="card-header-icon" aria-label="more options">
      <span class="icon">
        <i class="fas fa-angle-down" aria-hidden="true"></i>
      </span>
    </button>
  </header>
  <div class="card-content">
    <div class="content">
     {{post.message}} 
      
     
      <!-- <time datetime="2016-1-1">11:09 PM - 1 Jan 2016</time> -->
    </div>
  </div>
  <footer class="card-footer">
    <a @click="editPost(post._id)" class="card-footer-item">Edit</a>
    <a @click="deletePost(post._id)" class="card-footer-item">Delete</a>
    
  </footer>
</div>
<hr>
    </div>
</div>










</div>
</template>

<script>
import { onMounted } from 'vue';
import{reactive,ref} from 'vue'
import {useRouter} from 'vue-router'
import axios from 'axios'
export default {

setup(){
const router=useRouter()
const profile=reactive({
      name:'',
      username:'',
      email:'',
      createdAt:'',
    })
const API_URL="http://localhost:3000/profile/posts"    
const API_URL2="http://localhost:3000/posts" 
const posts2 = ref([]);   

  onMounted(()=>{
  validation();
  getProfile();
  getPosts2();
})
function validation(){
          if(localStorage.getItem('token')===null){
            alert('You need to be logged in before you access the content..')
          router.push({
            name:'Login',
          })}
        
        }
  async function getPosts2(){
    
    await axios.get(API_URL,{headers: {token:localStorage.getItem('token')}}).then((response)=>{
      const result= response.data;
      posts2.value=result;
    })

  }

async function getProfile() {
      await axios
          .get('http://localhost:3000/profile',{headers: {token:localStorage.getItem('token')}})
          .then((response) => (
            profile.name = response.data.name,
            profile.username = response.data.userName,
            profile.email = response.data.email,
            profile.createdAt = response.data.createdAt
            ))
          .catch(error => {
            console.log(error);
          });
      }
async function getPost2(_id){


    router.push({
            name:'Post',
            params:{
              id:_id,
            },
          })




}      
function editPost(_id){
  router.push({
    name:'Update',
    params:{
      id:_id
    }
  })

}
async function deletePost(_id){
 await axios.delete(`${API_URL2}/${_id}`);
 getPosts2();
 }
return{
  getProfile,
  profile,
  getPosts2,
  posts2,
  getPost2,
  deletePost,
  editPost,
  validation,
}
}
}

</script>

<style>

</style>