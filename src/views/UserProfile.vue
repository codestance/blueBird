<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ state.user.username }}</h1>
      <!-- <p>{{userId}}</p> -->
      <div class="user-profile__admin-badge" v-if="state.user.isAdmin">
          Admin
      </div>
      <div class="user-profile__follower-count">
        <p>Followers: {{ state.followers }}</p>
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
import {reactive, computed} from 'vue';
import {useRoute} from 'vue-router';
import {users} from '../assets/users';
import TweetItem from '@/components/TweetItem.vue';
import CreateNewTweet from '@/components/CreateNewTweet.vue'
export default {
  name: 'UserProfile',
  components: {
      TweetItem,
      CreateNewTweet
  },
  setup() {
    const route = useRoute();
    const userId = computed(() => route.params.userId)


    const state = reactive ({
      followers: 5,
      user: users[userId.value -1] || users[0]
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
      addTweet,
      userId
    }
  }
}
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  position: relative;
  padding: 2em;
  margin: 3em;
  border-radius: 1em;
  background: linear-gradient(115.04deg, rgba(255, 255, 255, 0.48) 1.5%, rgba(255, 255, 255, 0.12) 100%);
  backdrop-filter: blur(1em);
  z-index: 2;
  .user-profile__user-panel{
    display: flex;
    flex-direction: column;
    margin-right: 1em;
    padding: 1em;
    border-radius: .5em;
    background: linear-gradient(115.04deg, rgba(255, 255, 255, 0.48) 1.5%, rgba(255, 255, 255, 0.12) 100%); 
  }
  .user-profile__username{
    margin-bottom: .5em;
  }
  .user-profile__admin-badge{
      background-color:#F174FD;
      color:white;
      border-radius: 5px;
      margin-right: auto;
      padding: 5px;
  }
}
</style>
