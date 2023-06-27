<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg">
      <div class="container">
        <router-link to="/" class="navbar-brand">E-Book</router-link>
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <router-link to="/" class="nav-link">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/books" class="nav-link">Book List</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/categories" class="nav-link">Categories</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/member" class="nav-link">Member List</router-link>
          </li>
            <li class="nav-item">
                <router-link to="/desc" class="nav-link">Description</router-link>
            </li>
        </ul>
      </div>
    </nav>
    <div class="container mt-4">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
}
.navbar-brand{
  border: 5px solid #d7d5d5;
  padding: 5px 10px;
  border-radius: 20px;
  text-decoration: none;
  color: white;
}
.navbar-expand-lg {
    background-color: #9f9f9f;
}
</style>
