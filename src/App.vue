<template>
  <div id="app">
    <nav>
      <router-link to="/">
        Birds Social App
      </router-link>
    </nav>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
}

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color:#4D3DE3;
  min-height: 100vh;
  background: linear-gradient(252.44deg, #AC80FA 0%, #F174FD 100%);
}
nav{
  display:flex;
  padding: 1em;
  background: linear-gradient(115.04deg, rgba(255, 255, 255, 0.48) 1.5%, rgba(255, 255, 255, 0.12) 100%);
  a{
    color: white;
    text-decoration: none;
    font-weight: bolder;
  }
}
</style>
