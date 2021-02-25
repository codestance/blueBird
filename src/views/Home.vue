<template>
  <div class="home">
    <h1>Bird's Social App Home Page</h1>
    <div class="circle circle1"></div>
    <div class="circle circle2"></div>
    <div class="circle circle3"></div>
    <div class="users-list">
      <h2>Our most active users: </h2>
      <router-link v-for="user in users" :to="{ name: 'UserProfile', params: {userId: user.id} }" :key="user.id">
        {{ user.username }}
      </router-link>
    </div>
  </div>
</template>

<script>
import {users} from "../assets/users";
export default {
  name: 'Home',
  setup() {
    return {
      users
    }
  }
}
</script>
<style scoped lang="scss">
.home{
  padding: 1em;
  text-align: center;
  position: relative;
  h1{
    color: #67268b;
  }
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
    top: 45%;
    left: 55%;
  }
  .circle3{
    width: 8em;
    height: 8em;
    top: 90%;
    left: 30%;
  }
}
.users-list{
  display:flex;
  flex-direction: column;
  padding: 1em;
  border-radius: 1em;
  width: fit-content;
  margin: 0 auto;
  background: linear-gradient(115.04deg, rgba(255, 255, 255, 0.48) 1.5%, rgba(255, 255, 255, 0.12) 100%);
  backdrop-filter: blur(1em);
  z-index: 2;
  a{
    color: #8512c3;
    font-weight: bolder;
    text-decoration: none;
    margin: .5em 0;
  }
}
</style>