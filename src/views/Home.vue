<template>
  <div class="home">
    <h1>Bird's Social App Home Page</h1>
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
  z-index: 2;
  h1{
    color: #67268b;
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
  a{
    color: #8512c3;
    font-weight: bolder;
    text-decoration: none;
    margin: .5em 0;
    &:hover, &:active{
      color:#4D3DE3;
    }
  }
}
</style>