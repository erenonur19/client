<template>
<div class="container">
    <br>
    
  <div class="field">
  <label class="label">Name</label>
  <div class="control">
    <input class="input" type="text" placeholder="Text input">
  </div>
</div>

<div class="field">
  <label class="label">Username</label>
  <div class="control has-icons-left has-icons-right">
    <input class="input is-success" type="text" placeholder="Text input" value="bulma">
    <span class="icon is-small is-left">
      <i class="fas fa-user"></i>
    </span>
    <span class="icon is-small is-right">
      <i class="fas fa-check"></i>
    </span>
  </div>
  <p class="help is-success">This username is available</p>
</div>

<div class="field">
  <label class="label">Email</label>
  <div class="control has-icons-left has-icons-right">
    <input class="input is-danger" type="email" placeholder="Email input" value="hello@">
    <span class="icon is-small is-left">
      <i class="fas fa-envelope"></i>
    </span>
    <span class="icon is-small is-right">
      <i class="fas fa-exclamation-triangle"></i>
    </span>
  </div>
  <p class="help is-danger">This email is invalid</p>
</div>
 <div class="field">
  <label class="label">Password</label>
  <div class="control">
    <input class="input" type="password" placeholder="********">
  </div>
</div>
<br>


<div class="field is-grouped">
  <div class="control">
    <button class="button is-black">Register</button>
  </div>
  <div class="control">
    <button class="button is-danger">Cancel</button>
  </div>
</div>
</div>
</template>

<script>
export default {

}
</script>

<style>

</style>