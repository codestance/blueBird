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
      <form class="user-profile__create-tweet" @submit.prevent="createNewTweet">
        <label for="newTweet">New Tweet</label>
        <textarea id="newTweet" rows="5" v-model="newTweetContent"></textarea>
        <div class="user-profile__create-tweet-type">
          <label for="newTweetType">Type</label>
          <select id="newTweetType" v-model="selectedTweetType">
            <option :value="option.value"
              v-for="(option,index) in tweetTypes"
              :key="index"
            >
              {{ option.name }}
            </option>
          </select>
        </div>
        <button>Tweet!</button>
      </form>
    </div>
    <div class="user-profile__tweets-wrapper">
        <TweetItem class="user-profile__tweet"
            v-for="tweet in user.tweets"
            :key="tweet.id"
            :username="user.username"
            :tweet="tweet"
            @favourite="toggleFavourite"
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
        username:'bluebird',
        firstName: 'Blue',
        lastName: 'bird',
        email: 'email@bluebird.com',
        isAdmin: true,
        tweets: [
            {id: 1, content:'Blue bird golden thoughts'},
            {id: 2, content:'Dont forget to drink water!'}
        ]
      },
      tweetTypes: [
        {value:'draft', name:'Draft'},
        {value:'instant', name:'Instant Tweet'}
      ],
      newTweetContent: '',
      selectedTweetType: 'instant'
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
    },
    toggleFavourite(id){
      console.log(`favourited tweet #${id}`)
    },
    createNewTweet(){
      if(this.newTweetContent && this.selectedTweetType!=='draft'){
        this.user.tweets.unshift({
          id: this.user.tweets.length + 1,
          content: this.newTweetContent
        })
      }
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
.user-profile__create-tweet{
  display: flex;
  flex-direction: column;
}
</style>
