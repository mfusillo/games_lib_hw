<template>
  <section>
    <games-list v-bind:games="filteredGames" v-bind:parentGameId="gameSelectedId"/>
    <game-details v-bind:game="renderGame" />
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
      gameSelectedId: null,
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

    eventBus.$on("game-selected", (gameSelectedId) => {
      this.gameSelectedId = gameSelectedId
    })

    eventBus.$on("search-typed", (searchTyped) =>{
      this.searchTyped = searchTyped
    })
  },

  computed:{
    renderGame(){
      return this.games.find(game => game.id === this.gameSelectedId)
    },
    filteredGames(){
      const foundGames = this.games.filter(game => {
        return game.name.toLowerCase().includes(this.searchTyped.toLowerCase())
      })
      if (foundGames.length === 0){
        this.gameSelectedId = "n/a"
        return [{name: "Not Found", id: "n/a"}]
      }
      this.gameSelectedId = foundGames[0].id
      return foundGames
    }
  },

  components: {
    'games-list': GamesList,
    'game-details': GameDetails
  }


}
</script>

<style>

h2{
  font-size: 2em;
}

h3{
  font-size: 1.8em;
}
body{
  font-family: 'Oswald', serif;
  background-color: #033F63;
  color: #FEDC97;

}

::selection {
  color: #033F63;
  background: #7C9885;
}

</style>
