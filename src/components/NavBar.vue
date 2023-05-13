<template>
    <nav class="main-nav">
      <div class="">
        <router-link :to="{name:'home'}">Projects</router-link>
      </div>
      <div class="">
        <router-link :to="{name : 'addprojects'}">Add Projects</router-link>
      </div>
    </nav>
  </template>
  
  <script>
  export default {};
  </script>
  
  <style>
  .main-nav {
      display: flex;
      justify-content: space-evenly;
      margin: 50px auto;
  }
  .main-nav a {
      text-decoration: none;
      border: 0;
      padding-bottom: 6px;
      color: rgba(128, 128, 128, 0.722);
  }
  a.router-link-active {
    color: rgb(104, 101, 101);
    border-bottom: 3px solid green;
  }
  </style>
  