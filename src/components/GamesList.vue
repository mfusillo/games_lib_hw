<template>
  <section class="search-bar">
    <h2>GAMES LIB</h2>
    <form v-on:submit.prevent>
      <input type="text" v-model="searchText" placeholder="Enter a name to search"><br>
      <select v-model="selectedGameId">
        <option selected disabled value="">Select a game</option>
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
      selectedGameId: this.parentGameId
    }
  },
  props: ['games', 'parentGameId'],
  watch: {
    selectedGameId(){
      eventBus.$emit("game-selected", this.selectedGameId)
    },
    searchText(){
      eventBus.$emit("search-typed", this.searchText)
    },
    parentGameId(){
      this.selectedGameId = this.parentGameId
    }

  }
}

</script>

<style lang="css" scoped>

input {
  background-color: #B5B682;
  font: 400 15px 'Oswald';
  width: 30%;
  border-radius: 5px;
  border-width: 1px;
  border-style: solid;
  border-color: rgb(166, 166, 166);
  border-image: initial;
  margin-bottom: 0.8em;
}

input:focus {
    outline-width: 0;
}

.search-bar {
  align-content: center;
}

select, option {
  background-color: #B5B682;
  font: 400 15px 'Oswald';
  width: 30.5%;
}

select:focus {
    outline-width: 0;
}

</style>
