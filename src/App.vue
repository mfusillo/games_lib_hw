<template>
  <games-list v-bind:games="games" />
</template>

<script>

import GamesList from './components/GamesList.vue'
export default {
  name: 'app',
  data(){
    return {
      games: []
    }
  },
  mounted(){
    fetch('https://api.rawg.io/api/games?dates=2019-01-01,2019-12-31&ordering=-added&page_size=40')
    .then(result => result.json())
    .then(data => this.games = data.results)
  },
  components: {
    'games-list': GamesList
  }
}
</script>

<style>

</style>
