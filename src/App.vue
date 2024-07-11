<template>
  <router-view />
</template>

<script>
export default {
  name: 'App',
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  padding: 0;
  margin: 0;
}

.logoEdit {
  width: 200px;
}

.register input,
.login input,
.add input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid skyblue;
}

.register button,
.button-link,
.button {
  width: 300px;
  height: 40px;
  border: 1px solid skyblue;
  background-color: skyblue;
  color: white;
  cursor: pointer;
  border-radius: 4px;
  transition: background-color 0.3s ease;
  text-decoration: none;
  display: inline-block;
  text-align: center;
  line-height: 40px;
  font-size: 15px;
  border: none;
}

.register button:hover,
.button-link:hover,
.button:hover {
  background-color: #0056b3;
}

.button-link {
  color: white;
}

body,
html {
  height: 100%;
  margin: 0;
}

.login,
.register {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  flex-direction: column;
}

.container {
  display: flex;
  height: 100%;
}

.left-side,
.right-side {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.left-side {
  background-color: #f0f0f0;
}

.right-side {
  background-image: url('./assets/bg.jpg');
  background-size: cover;
  background-position: center;
  object-fit: contain;
  max-width: 100%;
  max-height: 100%;
}
</style>
