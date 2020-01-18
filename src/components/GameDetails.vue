<template>
  <section class="game-info-wrapper" v-if="game">
      <div class="game-title-pic">
        <h2>{{game.name}}</h2>
        <img v-bind:src="game.background_image" alt="">
      </div>
      <div class="game-trailer">
        <h3>Play Trailer</h3>
        <video v-bind:src="game.clip.clip" controls></video>
      </div>
  </section>
</template>

<script>
export default {
  name: 'game-details',
  props: ['game']
}
</script>

<style lang="css" scoped>

section.game-info-wrapper{
  display: grid;
  grid-template-columns: 1fr 1fr;
}

div.game-trailer{
  display: inline-grid;
  text-align: -webkit-right
}

img{
  height: auto;
  width: 30rem;
}

video{
  height: auto;
  width: 30rem;
}

</style>
