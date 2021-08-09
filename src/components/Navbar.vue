<template>
  <nav class="navbar is-black" role="navigation" aria-label="main navigation">
  <div class="navbar-brand">
    <!-- <a class="navbar-item" href="https://bulma.io">
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSfBtXNjeuwZj7t8ND6RTkfBTTPy1egnIyOPw&usqp=CAU" width="100" height="35">
    </a> 
    <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
    </a>
  
    -->
    

    
  </div>

  <div id="navbarBasicExample" class="navbar-menu">
    <div class="navbar-start">
    <strong class="navbar-item">FORUMAPI</strong>    


    <a class="navbar-item" href="http://localhost:8080">
        <strong>Homepage</strong>
      </a>

      <a class="navbar-item" href="http://localhost:8080/posts">
        <strong>Posts</strong>
      </a>
      <a class="navbar-item" href="http://localhost:8080/create">
        <strong>New Post</strong>
      </a>
      
      
      
    </div>

    <div class="navbar-end">
      <div class="navbar-item">
        <div class="buttons">
          <a class="button is-white">
            
            <strong>Profile</strong>
          </a>
          <a class="button is-white">
            <strong>Log Out</strong>
          </a>
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