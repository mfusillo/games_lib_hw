<template>
  <section>
    <h2>games list</h2>
    <form v-on:submit.prevent>
      <input type="text" v-model="searchText">
      <select v-model="selectedGameId">
        <option v-bind:value ="game.id" v-for="game of games">{{game.name}}</option>
      </select>
    </form>
  </section>
</template>

<script>

import { eventBus } from '../main.js'

export default {
  name: 'games-list',
  data(){
    return{
      searchText: '',
      selectedGameId: null
    }
  },
  props: ['games'],
  watch: {
    selectedGameId(){
      eventBus.$emit("game-selected", this.selectedGameId)
    },
    searchText(){
      eventBus.$emit("search-typed", this.searchText)
    }

  }
}

</script>

<style lang="css" scoped>
</style>
