<template>
  <section>
    <games-list v-bind:games="games" />
    <game-details v-bind:gameSelectedId="gameSelected" v-bind:searchTyped="searchTyped" />
  </section>
</template>

<script>

import { eventBus } from './main.js'
import GamesList from './components/GamesList.vue'
import GameDetails from './components/GameDetails.vue'

export default {
  name: 'app',
  data(){
    return {
      games: [],
      gameSelected: null,
      searchTyped: ""
    }
  },
  mounted(){

    const urls = [
      'https://api.rawg.io/api/games?dates=2019-01-01,2019-12-31&ordering=-added&page_size=40',
      'https://api.rawg.io/api/games?dates=2019-01-01%2C2019-12-31&ordering=-added&page=2&page_size=40'
    ]

    Promise.all(urls.map(url =>
      fetch(url)
      .then(result => result.json())
      .then(data => this.games = [...this.games,...data.results])
      )
    )

    eventBus.$on("game-selected", (gameSelected) => {
      this.gameSelected = gameSelected
    })

    eventBus.$on("search-typed", (searchTyped) =>{
      this.searchTyped = searchTyped
    })
  },
  components: {
    'games-list': GamesList,
    'game-details': GameDetails
  }


}
</script>

<style>

</style>
