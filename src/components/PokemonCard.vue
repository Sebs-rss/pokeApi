// Aquí se mostrarán cada Pokemon individualmente
<template>
  <div class="poke-card">
    <div>
      <img 
        :src="pokemonImage" 
        :style="imageStyle" 
        alt="Pokemon"
      />
    <div v-if="!discovered" class="poke-form">
      <input 
        v-model="inputName"
        class="poke-input"
        @keyup.enter="checkName"
      />
      <button class="poke-btn" @click="checkName">Descubrir</button>
    </div>
    <div v-else>
      <p>{{ pokemon.name }}</p>
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios';

    export default {
        name: 'PokemonCard',
        props: ['pokemon'],
        data() {
            return {
            pokemonImage: '',
            inputName: '',
            discovered: false
            };
        },
        
        // Aquí se usará una propiedad computada (funciones que se calculan en función de las propiedades reactivas del componente) para manejar el estilo de la imagen del Pokémon mediante transoformaciones CSS. Computed hace que se actualice automáticamente al detectar cambios en el componente. Es similar a función 'data' pero las propiedades computadas devuelven un valor.
        computed: {
        imageStyle() {
        return this.discovered ? '' : 'filter: blur(5px) grayscale(60%);';
        }
        },
        methods: {
        fetchPokemonDetails() {
          axios.get(this.pokemon.url)
            .then(response => {
              this.pokemonImage = response.data.sprites.front_default; // Cambiar aquí el tipo de imagen, puede ser estática en distintos tamaños o un gif
            })
            .catch(error => {
              console.error(error);
            });
        },
        checkName() {
        if (this.inputName.toLowerCase() === this.pokemon.name.toLowerCase()) {
          this.discovered = true;
          this.$emit('discovered');
        } else {
          alert('Nombre incorrecto');
        }
      }
    },
    // Aquí un lifecycle hook: "created", que se ejecuta antes de que el componente se monte en el DOM
    created() {
    this.fetchPokemonDetails();
    }
    }
</script>

<style scoped>
.poke-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  /* background-color: #fff; */
  border-radius: 10px;
  border: solid 1px #ccc;
  width: 200px;
  height: 225px;
  }

  .poke-btn {
    background-color:#117554;
    width: 100%;
  }

  .poke-form {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: .25rem;
    padding-bottom: .2rem;
  }

  .poke-input {
    background-color: #F5F5F7;
  }
</style>