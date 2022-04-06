<!--In dit document zit scirpt code html en css code. het is overzichtelijker als je het in aparte bestanden zet-->
<script>
  export default {
    data() {
      return {
        loading: true,
        pokemon: null,
        error: null,
        fotoUrl: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/",
        counter: [0,1,2,3,4,5,6,7,8,9]
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
    <div class="bovenkant">
      <div class="naam">{{ pokemon.name }}</div>
      <div class="hp">HP</div>
    </div>
      <div class="foto-pokemon">
         <img :src="fotoUrl + counter[1] + '.png'">  <!-- Ik wil met een loop door array heen loopen maar werkt nog niet -->
      </div>
    </div>
    
  </div>
</template>

<style>

.pokemon-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-gap: 100px;
  padding-left: 5%;
  padding-right: 5%;
}

.pokemoncard {
  height: 500px;
  line-height: 60px;
  border-radius: 15px;
  background-color: #0a3172;
  color: white;
  border: none;
  font-weight: 700;
  border: 10px solid #e2c40c;
}

.naam:first-letter {
  text-transform: capitalize;
}

.bovenkant {
  display: flex;
}

.naam {
  padding-left: 4%;
  height: 40px;
  line-height: 40px;
}

.hp {
  height: 40px;
  line-height: 40px;
  float: right;
  margin-left: auto;
  padding-right: 4%;
}

.foto-pokemon {
  height: 200px;
  background: #f2f2f2;
  border-radius: 5px;
  margin-left: 4%;
  margin-right: 4%;
}
</style>
