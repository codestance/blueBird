<template>
  <div class="tweet-item" @click="favouriteTweet(tweet.id)">
      <div class="tweet-item__container">
          <div class="tweet-item__user">
              @{{ username }}
          </div>
          <div class="tweet-item__content">
              {{ tweet.content }}
          </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'TweetItem',
  props:{
      username: {
          type: String,
          required: true
      },
      tweet: {
          type: Object,
          required: true
      }
  },
}
</script>

<style lang="scss" scoped>
.tweet-item {
  padding: 1em;
  border-radius: .5em;
  background: linear-gradient(94.01deg, rgba(255, 255, 255, 0.6) 0%, #FFFFFF 98.96%);
  cursor: pointer;
  transition: all .25s ease;
  margin-bottom: .5em;
  &:hover{
    transform: scale(1.01);
    }
  .tweet-item__container{
    
    .tweet-item__user{
      font-weight: bold;
    }
  }
}
</style>
