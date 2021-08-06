<template>
  <nav class="navbar is-dark" role="navigation" aria-label="main navigation">
  <div class="navbar-brand">
    <!-- <a class="navbar-item" href="https://bulma.io">
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSfBtXNjeuwZj7t8ND6RTkfBTTPy1egnIyOPw&usqp=CAU" width="100" height="35">
    </a> -->
    

    <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
    </a>
  </div>

  <div id="navbarBasicExample" class="navbar-menu">
    <div class="navbar-start">
    <strong class="navbar-item">FORUM API</strong>    
      <a class="navbar-item" href="http://localhost:8080/">
        Home
      </a>
      <a class="navbar-item" href="http://localhost:8080/create">
        New Post
      </a>
      
      
      
    </div>

    <div class="navbar-end">
      <div class="navbar-item">
        <div class="buttons">
          <!-- <router-link to="/create" class="button is-warning">
            <strong>Create Post</strong>
          </router-link> -->
         
        </div>
      </div>
    </div>
  </div>
</nav>
</template>

<script>
export default {

}
</script>

<style>

</style>