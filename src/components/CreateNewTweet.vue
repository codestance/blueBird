<template>
    <form class="create-tweet"
        @submit.prevent="createNewTweet"
        :class="{'--exceeded': newTweetCharCount > 200}"
    >
        <label for="newTweet">New Tweet {{ newTweetCharCount }}/200</label>
        <textarea id="newTweet" rows="6" v-model="state.newTweetContent"></textarea>
        <div class="create-tweet-type">
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
.create-tweet{
    display: flex;
    flex-direction: column;
    &.--exceeded{
      border-color: red;
      color: red;
    }
    textarea{
        border-radius: 1em;
        border: none;
    }
    button{
        padding: .5em;
        border-radius: 1em;
        border: none;
        background: linear-gradient(252.44deg, #AC80FA 0%, #F174FD 100%);
        color: white;
        font-weight: bolder;
    }
    .create-tweet-type{
        margin: .5em 0;
        label{
            padding-right: 1em;
        }
        select{
            padding: .5em;
            border-radius: 1em;
            border: none;
            width: 100%;
        }
        option{
            padding: .5em;
            border-radius: 1em;
        }
    }
}
</style>