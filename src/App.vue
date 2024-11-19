<script>
import PokemonList from './components/PokemonList.vue';

export default {
  name: 'App',
  components: {
    PokemonList
  }
}

</script>

<template>
  <div id="app">
    <h1>¿Quién es ese Pokémon?</h1>
    <PokemonList />
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
