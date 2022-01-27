<template>
  <img :src="enlace" alt="Not found" v-show="enlace!=null"/>
  <h2>{{name}}</h2>
  <div class="contenedor-opciones">
    <input type="text" placeholder="Ingrese un ID de Pokemon" v-model="nid" />
    <button @click="consultarPokemon">Consultar</button>
  </div>
</template>

<script>
export default {
  name: "PokemonOpciones",
  //"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg"

  props: {
    url: {
      type: String,
      default: null,
    },
    id: {
      type: Number,
      default: null,
    },
  },

  data() {
    return {
      enlace: null,
      nid: null,
      name: ""
    }
  },
  methods: {
    async nombrePokemon() {
      const pokemon = await fetch(`https://pokeapi.co/api/v2/pokemon/${this.nid}`).then(r=>r.json())
      return pokemon.name
    },
    async consultarPokemon() {
      console.log("Este es el id: " + this.id);
      this.enlace =
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/" +
        this.nid +
        ".svg";
      this.name = await this.nombrePokemon()
    },
  },

};
</script>

<style>
button {
  cursor: pointer;
  background-color: rgba(0, 0, 0, 0.2);
}

input,
button {
  margin-right: 5px;
  border-radius: 5px;
}

button:hover {
  background-color: aqua;
}

.contenedor-opciones {
  display: flex;
  justify-content: center;
}

img {
  margin: 20px;
}
</style>