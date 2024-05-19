<template>
    <aside class="sidebar" tabindex="0">
      <ul>
        <li><nuxt-link to="/">Home</nuxt-link></li>
        <li><nuxt-link to="/">About</nuxt-link></li>
        <!-- Add more sidebar links as needed -->
      </ul>
    </aside>
  </template>
  
  <script setup>
  // No script needed for this example
  </script>
  
  <style scoped>
  .sidebar {
    width: 250px;
    height: 100%;
    background-color: #f0f0f0;
    padding: 20px;
    position: fixed;
    left: 0;
    top: 0;
    bottom: 0;
    outline: none; /* Remove outline when sidebar is focused */
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    margin: 10px 0;
  }
  
  a {
    text-decoration: none;
    color: inherit;
  }
  
  a:focus {
    background-color: #ddd; /* Highlight focused link */
  }
  </style>
  