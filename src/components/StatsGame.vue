<template>
    <div class="stats">
        <div class="total">
            <p>Total: {{ stats.total }} / {{ stats.max }}</p>
        </div>

        <div class="left">
            <p>Correctas: {{ stats.correct }} / {{ stats.total }}</p>
        </div>

        <div class="right">
            <p>Incorrectas: {{ stats.fail }} / {{ stats.total }}</p>
        </div>
        <div class="chance">
            <p>Oportunidades: {{ stats.chance }} / {{ stats.chanceMax }}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        statsGame: {
            type: Array
        }
    },
    data() {
        return {
            stats: [
                {
                    correct: 0,
                    fail: 0,
                    total: 0,
                    chance: 0,
                    max: 0,
                    chanceMax: 0,
                }
            ],
        }
    },
    watch: {
        stats:()=>{
            console.log(this.stats.correct, this.statsGame.correct)
        }
    }
}
</script>

<style scoped>
.stats {
  position: absolute;
  top: 45%;
  display: flex;
  flex-direction: column;
  justify-items: center;
  margin: 0 0 0 10px;
  padding: 10px;
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