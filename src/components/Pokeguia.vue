<template>
  <div>
    <form @submit.prevent="buscarPokemon" class="form-inline mt-5">
      <div class="form-group mx-sm-3 mb-2">
        <label for="search" class="sr-only">Busca tu Pokemon!</label>
        <input type="text" class="form-control" id="search" placeholder="Ingrese aquí el nombre" v-model="nombre_pokemon">
      </div>
      <button type="submit" class="btn btn-primary mb-2">Buscar</button>
    </form>
    <div class="text-center">
      <div class="d-flex justify-content-around">
        <p v-if="nombre_pokemon.length == 0" class="display-4">{{name_pikachu}} </p>
        <p v-else class="display-4">{{nombre_pokemon}} </p>
        <img class="" :src="buscarImagen">
      </div>
      <div>
        <h2>Movimiento</h2>
        <p>{{buscarMovimientos}}</p>
      </div>
      <div>
        <h2>Habilidades</h2>
        <ul v-for="(hab, index) in buscarHabilidades" :key="index">
          <li>{{hab.ability.name}}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Pokeguia',
  data() {
    return {
      nombre_pokemon: '',
      resultado: '',
      name_pikachu: '',
      imagen: '',
      moves:'',
      habilidades: []
    }
  },
  methods: {
    buscarPokemon(){
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.nombre_pokemon} `)
      .then(resp => resp.json())
      .then(result => {
        this.resultado = result;
        this.nombre_pokemon = result.name;
        this.imagen = result.sprites.front_default;
        this.moves = result.moves[0].move.name;
        this.habilidades = result.abilities;
      })
      .catch(error => console.error(error))
    },
  },
  computed: {
    buscarHabilidades(){
      return this.habilidades;
    },
    buscarMovimientos(){
      return this.moves;
    },
    buscarImagen(){
      return this.imagen;
    }
  },
  created() {
    fetch('https://pokeapi.co/api/v2/pokemon/pikachu')
      .then(resp => resp.json())
      .then(result => {
        this.name_pikachu = result.name;
        this.imagen = result.sprites.front_default;
        this.moves = result.moves[0].move.name;
        this.habilidades = result.abilities;
      }) 
      .catch(error => console.error(error))
  
  },
}
</script>


<style scoped>
form{
  margin-left: 40%;
}
li{
  list-style-position: inside;
}
</style>
