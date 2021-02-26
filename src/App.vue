<template>
  <div id="app">
    <nav>
      <router-link to="/">
        Birds Social App
      </router-link>
      <p>{{ user.username }}</p>
    </nav>
    <router-view/>
    <div class="circle circle1"></div>
    <div class="circle circle2"></div>
    <div class="circle circle3"></div>
  </div>
</template>

<script>
import { useStore } from 'vuex';
import { computed } from 'vue';
export default {
  name: 'App',
  setup() {
    const store = useStore();
    const user = computed(() => store.state.user);
    return {
      user
    }
  }
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
  .circle{
    background: linear-gradient(115.04deg, rgba(255, 255, 255, 0.6) 1.5%, rgba(255, 255, 255, 0.12) 100%, rgba(255, 255, 255, 0) 100%);
    border-radius: 50%;
    position:absolute;
  }
  .circle1{
    width: 5em;
    height: 5em;
    top: 10%;
    left: 15%;
  }
  .circle2{
    width: 12em;
    height: 12em;
    top: 40%;
    left: 55%;
  }
  .circle3{
    width: 8em;
    height: 8em;
    top: calc(95% - 8em);
    left: 30%;
  }
}
nav{
  display:flex;
  justify-content:space-between;
  color: white;
  font-weight: bolder;
  padding: 1em;
  background: linear-gradient(115.04deg, rgba(255, 255, 255, 0.48) 1.5%, rgba(255, 255, 255, 0.12) 100%);
  a{
    text-decoration: none;
  }
}
</style>
