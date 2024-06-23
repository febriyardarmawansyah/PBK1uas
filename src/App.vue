<template>
  <div class="container">
    <header>
      <nav>
        <ul>
          <li>
            <router-link to="/posts" class="btn-3d">Posts</router-link>
          </li>
          <li>
            <router-link to="/todos" class="btn-3d">Todos</router-link>
          </li>
          <li>
            <router-link to="/albums" class="btn-3d">Albums</router-link>
          </li>
        </ul>
      </nav>
    </header>
    <div class="content">
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 10px;
  min-height: 100vh;
}

header {
  background-color: #0ff94e;
  padding: 10px;
  border-radius: 5px;
  width: 100%;
  max-width: 800px;
}

nav ul {
  list-style: none;
  display: flex;
  justify-content: space-around;
  padding: 0;
  margin: 0;
}

nav ul li {
  margin: 0 5px;
}

.router-link {
  color: #fff;
  text-decoration: none;
  padding: 5px 10px;
  border-radius: 3px;
  transition: background-color 0.3s;
}

.router-link:hover {
  background-color: #cc00cc;
}

.content {
  width: 100%;
  max-width: 800px;
  margin-top: 20px;
}

/* 3D Button Styles */
.btn-3d {
  display: inline-block;
  padding: 10px 20px;
  margin: 10px;
  color: #fff;
  background-color: #3a4c5f;
  text-align: center;
  text-decoration: none;
  border-radius: 8px;
  box-shadow: 0 4px #0056b3;
  transition: all 0.2s ease;
}

.btn-3d:active {
  box-shadow: 0 2px #0056b3;
  transform: translateY(2px);
}
</style>
