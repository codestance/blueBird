<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ state.user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="state.user.isAdmin">
          Admin
      </div>
      <div class="user-profile__follower-count">
        <p>Followers {{ state.followers }}</p>
        <!-- <button@click="followUser">Follow</button> -->
      </div>
      <CreateNewTweet @add-tweet="addTweet"></CreateNewTweet>
    </div>
    <div class="user-profile__tweets-wrapper">
        <TweetItem class="user-profile__tweet"
            v-for="tweet in state.user.tweets"
            :key="tweet.id"
            :username="state.user.username"
            :tweet="tweet"
        >
            {{tweets.content}}
        </TweetItem>
    </div>
  </div>
</template>

<script>
import {reactive} from 'vue';
import TweetItem from '@/components/TweetItem.vue';
import CreateNewTweet from '@/components/CreateNewTweet.vue'
export default {
  name: 'userProfile',
  components: {
      TweetItem,
      CreateNewTweet
  },
  setup() {
    const state = reactive ({
      followers: 0,
      user: {
        id: 1,
        username:'bluebird',
        firstName: 'Blue',
        lastName: 'bird',
        email: 'email@bluebird.com',
        isAdmin: true,
        tweets: [
            {id: 1, content:'Blue bird golden thoughts'},
            {id: 2, content:'Dont forget to drink water!'}
        ]
      }
    })

    function addTweet(tweet){
      state.user.tweets.unshift(
        {
          id: state.user.tweets.length + 1,
          content: tweet
        }
      )
    }

    return {
      state,
      addTweet
    }
  }
}
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
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
}
</style>
