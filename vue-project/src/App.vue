<!--In dit document zit scirpt code html en css code. het is overzichtelijker als je het in aparte bestanden zet-->
<script>
  export default {
    data() {
      return {
        loading: true,
        pokemon: null,
        error: null,
      }
    },
    created() {
      //api call uitvoeren
      this.fetchData()
    },
    //Api call om pokemons op te halen
    methods: {
      fetchData() {
        this.error = this.post = null
        this.loading = true
        fetch('https://pokeapi.co/api/v2/pokemon?limit=151').then(res => res.json()).then(data => {
          this.loading = false;
          //variabele van alle pokemons
          this.pokemon = data.results;
        })
      },
    },
  }
</script>
<template>
  <div v-if="loading">LOADING</div>
  <div class="pokemon-grid">
<!--    alle opgehaalde pokemons laten zien-->
<!--    pokemon variabele word gebruikt van functie fetchData()-->
    <div class="pokemoncard" v-for="pokemon in pokemon" :key="pokemon.name">
      {{ pokemon.name }}
    </div>
  </div>
</template>

<style>
/*style van grid om pokemons te tonen*/
.pokemon-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 20px;
  text-align: center;
}

.pokemoncard {
  height: 60px;
  line-height: 60px;
  border-radius: 15px;
  background-color: #DC143C;
  color: white;
  border: none;
  font-weight: 700;
}
</style>
