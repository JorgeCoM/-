<template>
    <div v-if="!gameStart">
        <h2>Selecciona el modo de juego</h2>
        <div class="container-game">
            <button @click="$emit('selectionGame', items.mode, items.total, items.chance)" class="botton"
                v-for="(items, index) in modeGame" :key="index"> {{ items.mode }} </button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        gameStart: {
            type: Boolean
        }
    },
    data() {
        return {
            modeGame: [
                {
                    mode: "easy",
                    total: 10,
                    chance: 7
                },
                {
                    mode: "medium",
                    total: 30,
                    chance: 5
                },
                {
                    mode: "hard",
                    total: 50,
                    chance: 3
                },
                {
                    mode: "Master Pokemon",
                    total: 100,
                    chance: 3
                }
            ]
        }
    },
    methods: {
    }

}
</script>

<style scoped>
.container-game {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.botton {
    width: 150px;
    height: 50px;
    margin: 5px 0 5px 0;
    border: none;
    border-radius: 20px;

}

.botton:nth-child(1) {
    background-color: rgb(0, 213, 255);
    border: 2px solid rgb(25, 141, 199);
}

.botton:nth-child(2) {
    background-color: rgb(47, 255, 0);
    border: 2px solid rgb(31, 199, 25);
}

.botton:nth-child(3) {
    background-color: rgb(206, 59, 26);
    border: 2px solid rgb(175, 67, 17);
}

.botton:nth-child(4) {
    background-color: rgb(136, 0, 255);
    border: 2px solid rgb(153, 25, 199);
}
</style>