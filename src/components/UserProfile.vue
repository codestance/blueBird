<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">
          Admin
      </div>
      <div class="user-profile__follower-count">
        <p>Followers {{ followers }}</p>
        <!-- <button@click="followUser">Follow</button> -->
      </div>
    </div>
    <div class="user-profile__tweets-wrapper">
        <TweetItem class="user-profile__tweet"
            v-for="tweet in user.tweets"
            :key="tweet.id"
            :username="user.username"
            :tweet="tweet"
        >
            {{tweets.content}}
        </TweetItem>
    </div>
  </div>
</template>

<script>
import TweetItem from '@/components/TweetItem.vue';
export default {
  name: 'userProfile',
  components: {
      TweetItem
  },
  data() {
    return{
      followers: 0,
      user: {
        id: 1,
        username:'codestance',
        firstName: 'Connie',
        lastName: 'Stance',
        email: 'email@email.com',
        isAdmin: true,
        tweets: [
            {id: 1, content:'Blue bird golden thoughts'},
            {id: 2, content:'Dont forget to drink water!'}
        ]
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount){
      if(oldFollowerCount < newFollowerCount){
        console.log(`${this.user.username} has gained a follower`)
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`
    }
  },
  methods: {
    followUser() {
      this.followers++
    }
  },
  mounted() {
    this.followUser()
  }
}
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}
.user-profile__user-panel{
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
}
.user-profile__admin-badge{
    background-color: red;
    color:white;
    border-radius: 5px;
    margin-right: auto;
    padding: 5px;
}
</style>
