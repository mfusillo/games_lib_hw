<template>
  <ul>
    <li v-for="game of games">{{game.name}}</li>
  </ul>
</template>

<script>
export default {
  name: 'games-list',
  props: ['games']
}
</script>

<style lang="css" scoped>
</style>
