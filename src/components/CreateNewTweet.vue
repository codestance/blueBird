<template>
    <form class="user-profile__create-tweet"
        @submit.prevent="createNewTweet"
        :class="{'--exceeded': newTweetCharCount > 200}"
    >
        <label for="newTweet">New Tweet {{ newTweetCharCount }}/200</label>
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
</template>

<script>
export default{
    name: 'CreateNewTweet',
    data() {
        return{
            tweetTypes: [
                {value:'draft', name:'Draft'},
                {value:'instant', name:'Instant Tweet'}
            ],
            newTweetContent: '',
            selectedTweetType: 'instant'
        }
    },
    computed: {
        newTweetCharCount(){
            return this.newTweetContent.length;
        }
    },
    methods: {
        createNewTweet(){
            if(this.newTweetContent && this.selectedTweetType!=='draft'){
                // this.user.tweets.unshift({
                //     id: this.user.tweets.length + 1,
                //     content: this.newTweetContent
                // });
                this.$emit('add-tweet', this.newTweetContent);
                this.newTweetContent = '';
            }
        }
    }
}
</script>

<style lang="scss" scoped>
.user-profile__create-tweet{
    display: flex;
    flex-direction: column;
    &.--exceeded{
      border-color: red;
      color: red;
    }
    .user-profile__create-tweet-type{
        margin: .5em 0;
        label{
            padding-right: 1em;
        }
    }
}
</style>