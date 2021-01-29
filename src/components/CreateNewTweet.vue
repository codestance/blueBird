<template>
    <form class="user-profile__create-tweet"
        @submit.prevent="createNewTweet"
        :class="{'--exceeded': newTweetCharCount > 200}"
    >
        <label for="newTweet">New Tweet {{ newTweetCharCount }}/200</label>
        <textarea id="newTweet" rows="5" v-model="state.newTweetContent"></textarea>
        <div class="user-profile__create-tweet-type">
          <label for="newTweetType">Type</label>
          <select id="newTweetType" v-model="state.selectedTweetType">
            <option :value="option.value"
              v-for="(option,index) in state.tweetTypes"
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
import { reactive, computed } from 'vue';
export default{
    name: 'CreateNewTweet',
    setup(props,ctx) {
        const state= reactive ({
            tweetTypes: [
                {value:'draft', name:'Draft'},
                {value:'instant', name:'Instant Tweet'}
            ],
            newTweetContent: '',
            selectedTweetType: 'instant'
        })
        
        const newTweetCharCount = computed(() => state.newTweetContent.length)

        function createNewTweet(){
            if(state.newTweetContent && state.selectedTweetType!=='draft'){
                ctx.emit('add-tweet', state.newTweetContent);
                state.newTweetContent = '';
            }
        }

        return {
            state,
            newTweetCharCount,
            createNewTweet
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