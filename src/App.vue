<template>
  <div id="app">
<<<<<<< HEAD
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
=======
    <nav class="navbar navbar-expand-lg">
>>>>>>> f7d0455 (commit)
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
<<<<<<< HEAD
            <router-link to="/Member" class="nav-link">Member List</router-link>
          </li>
=======
            <router-link to="/member" class="nav-link">Member List</router-link>
          </li>
            <li class="nav-item">
                <router-link to="/desc" class="nav-link">Description</router-link>
            </li>
>>>>>>> f7d0455 (commit)
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
<<<<<<< HEAD
  border: 1px solid #ffffff;
=======
  border: 5px solid #d7d5d5;
>>>>>>> f7d0455 (commit)
  padding: 5px 10px;
  border-radius: 20px;
  text-decoration: none;
  color: white;
}
<<<<<<< HEAD
=======
.navbar-expand-lg {
    background-color: #9f9f9f;
}
>>>>>>> f7d0455 (commit)
</style>
