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
      this.fetchData()
    },
    methods: {
      fetchData() {
        this.error = this.post = null
        this.loading = true
        // replace `getPost` with your data fetching util / API wrapper
        fetch('https://pokeapi.co/api/v2/pokemon?limit=151').then(res => res.json()).then(data => {
          this.loading = false;
          this.pokemon = data.results;
        })
      },
    },
  }
</script>

<template>
  <div v-if="loading">LOADING</div>
  <div class="pokemon-grid">
    <div class="pokemoncard" v-for="pokemon in pokemon" :key="pokemon.name">
      {{pokemon.name}}
    </div>
  </div>
</template>

<style>
.pokemon-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-gap: 20px;
}
</style>

