// Componente responsable de obtener y mostrar la lista de Pokémon
<template>
    <h2>Pokémones descubiertos: {{ discoveredCount }}</h2>
    <div class="pokemon-grid">
    <!-- @discovered corresponde a la escucha de un evento personalizado que se dispara cuando un pokemon es descubierto -->
    <PokemonCard 
      v-for="pokemon in pokemons" 
      :key="pokemon.name" 
      :pokemon="pokemon" 
      @discovered="handleDiscovered"
    />
    
  </div>
</template>

<script>
    import axios from 'axios';
    import PokemonCard from './PokemonCard.vue';
    
    export default {
        name: 'PokemonList',
        components: {
        PokemonCard
  },
  data() {
    return {
      pokemons: [],
      discoveredCount: 0
    };
  },

  methods: {
    fetchPokemons() {
      axios.get('https://pokeapi.co/api/v2/pokemon?limit=20')
        .then(response => {
          this.pokemons = response.data.results;
        })
        .catch(error => {
          console.error(error);
        });
    },
    // Contador de Pokemones descubiertos
    handleDiscovered() {
      this.discoveredCount++;
    }
  },
// Aquí un hook de ciclo de vida: "Created", se ejecutará después de que se ha creado la instancia del componente y se ha inicializado la reactividad, pero antes de que el componente se monte en el DOM. Llamará al método fetchPokemons tan pronto como se crea la instancia del componente
created() {
    this.fetchPokemons();
  }

    }
</script>

<style scoped>
.pokemon-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
/*   grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); */
  gap: .5rem;
}

</style>