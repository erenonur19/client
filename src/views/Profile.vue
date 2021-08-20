<template>
<div class="container">
  <div class="tabs is-centered is-medium is-boxed">
  <ul>
    <li class="tab is-active" @click="openTab(event,'About')"><a >About</a></li>
    <li class="tab" @click="openTab(event,'Posts'),getPosts2();"><a >Posts</a></li>
    <li class="tab" @click="openTab(event,'Comments')"><a >Comments</a></li>
  </ul>
</div>
<div>
  
<div class="container section">
    <div id="About" class="content-tab" >
      <div class="card">
  <div class="card-image">
    <figure class="image is-3by1">
      <img src="https://cdn.pixabay.com/photo/2015/10/05/22/37/blank-profile-picture-973460_960_720.png" alt="Placeholder image">
    </figure>
  </div>
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
    </div>
    <div v-for="post in posts2" :key="post.userName" id="Posts" class="content-tab" style="display:none">
       <div class="card">
  <header class="card-header">
    <p class="card-header-title">
      {{post.title}}
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
      <a href="#">@bulmaio</a>. <a href="#">#css</a> <a href="#">#responsive</a>
      <br>
      <time datetime="2016-1-1">11:09 PM - 1 Jan 2016</time>
    </div>
  </div>
  <footer class="card-footer">
    <a href="#" class="card-footer-item">Edit</a>
    <a href="#" class="card-footer-item">Delete</a>
  </footer>
</div>
    </div>
    <div id="Comments" class="content-tab" style="display:none">
       <div class="card">
  <header class="card-header">
    <p class="card-header-title">
      Component
    </p>
    <button class="card-header-icon" aria-label="more options">
      <span class="icon">
        <i class="fas fa-angle-down" aria-hidden="true"></i>
      </span>
    </button>
  </header>
  <div class="card-content">
    <div class="content">
      
      
      <br>
      <time datetime="2016-1-1">11:09 PM - 1 Jan 2016</time>
    </div>
  </div>
  <footer class="card-footer">
    <a href="#" class="card-footer-item">Edit</a>
    <a href="#" class="card-footer-item">Delete</a>
  </footer>
</div>
    </div>
</div>








</div>

</div>
</template>

<script>
import { onMounted } from 'vue';
import{reactive,ref} from 'vue'
import axios from 'axios'
export default {
setup(){
const profile=reactive({
      name:'',
      username:'',
      email:'',
      createdAt:'',
    })
const API_URL="http://localhost:3000/profile/posts"    
const posts2 = ref([]);   

  onMounted(()=>{
  getProfile();
  openTab();
  
  
})

  async function getPosts2(){
    
    await axios.get(API_URL,{headers: {token:localStorage.getItem('token')}}).then(async(response)=>{
      const result=await response.json();
      posts2.value=result;
    })

  }
  
  function openTab(evt, tabName) {
  var i, x, tablinks;
  x = document.getElementsByClassName("content-tab");
  for (i = 0; i < x.length; i++) {
      x[i].style.display = "none";
  }
  tablinks = document.getElementsByClassName("tab");
  for (i = 0; i < x.length; i++) {
      tablinks[i].className = tablinks[i].className.replace(" is-active", "");
  }
  document.getElementById(tabName).style.display = "block";
  evt.currentTarget.className += " is-active";
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
return{
  openTab,
  getProfile,
  profile,
  getPosts2,
  posts2,
}
}
}

</script>

<style>

</style>