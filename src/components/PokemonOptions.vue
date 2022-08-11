<template>
    <div class="options-container">
        <ul>
            <li :class="[validationStatus(id), '']" class="" v-for="{ name, id } in Pokemons"
                @click="$emit('selection', id, name)" :key="id">
                {{ name }}
            </li>
        </ul>
    </div>
    <div>
    </div>
</template>

<script>
export default {
    props: {
        Pokemons: {
            type: Array,
            required: true,
        },
        checkpokemon: {
            type: Array,
            default: [{
                chance: 1
            }]
        },
    },
    methods: {
        validationStatus(id) {
            if (this.checkpokemon === null) {
                return ''
            } else if (this.checkpokemon[0].id === id) {
                return 'green no__pointer'
            } else {
                return 'red no__pointer'
            }
        }
    }

}
</script>

<style scoped>
/* Pokemon Options */
ul {
    list-style-type: none;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 500px;
}

li {
    background-color: white;
    position: relative;
    right: 10px;
    border-radius: 5px;
    border: 1px solid rgba(0, 0, 0, 0.2);
    cursor: pointer;
    margin-bottom: 10px;
    width: 250px;
}

li:hover {
    background-color: rgba(0, 0, 0, 0.05);
}

.options-container {
    display: flex;
    justify-content: center;
}

.no__pointer {
    pointer-events: none;
}

.red {
    background-color: brown;
}

.green {
    background-color: greenyellow;
}
</style>