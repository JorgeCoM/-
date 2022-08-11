<template>
    <div class="pokemon-container">
        <img class="hidden-pokemon" :src="imgSrc" alt="Pokemon">
        <img class="fade-in" v-if="ShowPokemon" :src="imgSrc" alt="Pokemon">

    </div>


</template>

<script>
export default {
    props: {
        PokemonId: {
            type: Number,
            required: true,
            default: 1
        },
        ShowPokemon: {
            type: Boolean,
            required: true,
            default: false
        }
    },
    computed: {
        imgSrc() {
            return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.PokemonId}.svg`
        }
    }
}
</script>

<style scoped>
/* Pokemon Picture */
.pokemon-container {
    height: 200px;
    display: flex;
    justify-content: center;
    align-items: center;
}

img {
    height: 200px;
    position: absolute;
    user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    -webkit-user-drag: none;
    -webkit-user-select: none;
}

.hidden-pokemon {
    filter: brightness(0);
}
</style>