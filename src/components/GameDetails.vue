<template>
  <section v-if="game">
    <div class="game-info-wrapper">
      <div class="game-title-pic">
        <h2>{{game.name}}</h2>
        <img v-bind:src="game.background_image" alt="">
      </div>
      <div class="game-trailer">
        <h3>Play Trailer</h3>
        <video v-bind:src="game.clip.clip" controls></video>
      </div>
    </div>
      <div class="rating-buttons">
        Rate the game! <input type="radio" v-model="ratingScore" value="1">1
        <input type="radio" v-model="ratingScore" value="2">2
        <input type="radio" v-model="ratingScore" value="3">3
        <input type="radio" v-model="ratingScore" value="4">4
        <input type="radio" v-model="ratingScore" value="5">5
      </div>
  </section>
</template>

<script>

import { eventBus } from '../main.js'

export default {
  name: 'game-details',
  props: ['game', 'parentRatingScore'],
  data(){
    return{
      ratingScore: null
    }
  },
  watch: {
    ratingScore(){
      eventBus.$emit("rating-selected", this.ratingScore)
      }
    }
    // ,
    // parentRatingScore(){
    //   this.ratingScore = this.parentRatingScore
    // }
}
</script>

<style lang="css" scoped>


div.game-title-pic{
  text-align: center;
}

div.game-info-wrapper{
  display: grid;
  grid-template-columns: 1fr 1fr;
}

div.game-trailer{
  display: inline-grid;
  text-align: center;
}

img{
  height: auto;
  width: 30rem;
}

video{
  height: auto;
  width: 30rem;
}

div.rating-buttons{
  text-align: center;
  margin-top: 1rem;
}

</style>
