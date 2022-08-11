<template>
  <GameSelecctor :gameStart="gameStart" @selectionGame="checkGame"></GameSelecctor>
  <div v-if="gameStart">
    <h3 v-if="!pokemon">Cargando Pokémon...</h3>

    <div v-else>
      <h1>¿Quién es el pokémon?</h1>

      <PokemonPicture :PokemonId="pokemon.id" :ShowPokemon="showPokemon" />
      <PokemonOptions :checkpokemon="checkPokemonList" :Pokemons="pokemonArr" @selection="checkAnswer" />

      <div v-if="showAnswer">
        <h3 class="fade-in">{{ message }}</h3>
        <button @click="newGame">Nuevo juego</button>
      </div>
    </div>
  </div>
  <div v-if="stats" class="stats">
    <div class="total">
      <p>Total: {{ total }} / {{ max }}</p>
    </div>

    <div class="left">
      <p>Correctas: {{ correct }} / {{ total }}</p>
    </div>

    <div class="right">
      <p>Incorrectas: {{ fail }} / {{ total }}</p>
    </div>
    <div class="chance">
      <p>Oportunidades: {{ chance }} / {{ chanceMax }}</p>
    </div>
  </div>
        <p>Autor JorgeCoM | <a href="https://github.com/JorgeCoM?tab=repositories">Github</a></p>
</template>

<script>
import PokemonPicture from '@/components/PokemonPicture.vue'
import PokemonOptions from '@/components/PokemonOptions.vue'
import getPokemonOptions from "@/helpers/getPokemonOptions"
import GameSelecctor from '@/components/GameSelecctor.vue'

export default {
  components: {
    PokemonPicture,
    PokemonOptions,
    GameSelecctor
  },
  data() {
    return {
      gameStart: false,
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: '',
      correct: 0,
      fail: 0,
      total: 0,
      chance: 0,
      max: 0,
      chanceMax: 0,
      checkPokemonList: null,
      stats: false
    }
  },
  mounted() {
    this.mixPokemonArray()
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArr = await getPokemonOptions()
      const rndInt = Math.floor(Math.random() * 4)
      this.pokemon = this.pokemonArr[rndInt]
    },
    checkAnswer(pokemonId, name) {
      this.showAnswer = true
      if (pokemonId) {
        this.checkPokemonList = [{
          id: pokemonId,
          name: name,
          chance: 1
        }]
      }
      if (this.chance >= this.chanceMax || this.total == this.max) {
        this.gameStart = false
        this.stats = true
        this.newGame()
      }
      if (this.pokemon.id >= pokemonId) {
        this.showPokemon = true
        this.message = `Acertaste es ${this.pokemon.name}`
        this.correct++
        this.total++
        console.log(this.total, this.max)
      } else {
        this.message = `nop, es ${name} era ${this.pokemon.name}`
        this.fail++
        this.total++
        this.chance++
      }
    },
    newGame() {
      this.showPokemon = false
      this.showAnswer = false
      this.pokemonArr = []
      this.mixPokemonArray()
      this.pokemon = null
      this.checkPokemonList = null
    },
    checkGame(a, b, c) {
      if (a && b && c) {
        console.log(a, b, c)
        this.stats = false
        this.reset()
        this.gameStart = true
        this.max = b
        this.chanceMax = c
      }

    },
    reset() {
      this.chance = 0
      this.correct = 0
      this.fail = 0
      this.total = 0
    }

  }

}
</script>

<style scoped>
.stats {
  display: flex;
  flex-direction: column;
  justify-items: center;
  margin: 0 0 0 10px;
  padding: 10px;
  margin: 20px 0 0 0;
}

.left>p {
  color: rgba(6, 235, 6, .5);
  font-weight: 600;

}

.right>p {
  color: rgba(235, 6, 6, 0.5);
  font-weight: 600;

}

.total>p {
  font-weight: 600;
  color: rgba(11, 197, 221, 0.5);
}

.chance {
  font-weight: 600;
  color: rgba(221, 165, 11, 0.5);
}
</style>

