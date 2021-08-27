<template>
   <div class="container">
     <br>
     
     
 
 <form @submit.prevent="submitPost">
   <!-- <div class="field">
  <label class="label">Username</label>
  <div class="control">
    <input v-model="post.userName" class="input" type="text" placeholder="Text input" required>
  </div>
</div> -->

<div class="field">
  <label class="label">Title</label>
  <div class="control">
    <input v-model="post.title" class="input" type="text" placeholder="Text input" required minlength="3" maxlength="30">
  </div>
</div>


<div class="field">
  <label class="label">Message</label>
  <div class="control">
    <textarea v-model="post.message" class="textarea" placeholder="Textarea" required minlength="3" maxlength="900"></textarea>
  </div>
</div>


<div class="field is-grouped">
  <div class="control">
    <button type="submit" class="button is-black">Submit</button>
  </div>
  <div class="control">
    <button class="button is-danger">Cancel</button>
  </div> 
</div></form>


 </div>
</template>
<script>
import {useRouter} from 'vue-router'
export default {
    props:['post','submitPost']
  
         
  
}
</script>

<style>
</style>