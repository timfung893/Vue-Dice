<template>
    <div class="control-wrapper">
        <button class="control new-game-btn"
            v-on:click="initNewGame">
            <i class="ion-ios-plus-outline"></i>
            New Game
        </button>
        <button class="control roll-dice-btn" 
            v-on:click="rollDice">
           <i class="ion-ios-loop"></i>Roll Dice
        </button>
        <button class="control hold-btn"
            v-on:click="holdScore"
        >
            <i class="ion-ios-download-outline"></i>
            Hold

        </button>
        <input type="number" placeholder="Final Score" class="control final-score"
            v-on:input="$emit('changeFinalScore', $event)"
            v-bind:value="finalScore"
            v-bind:disabled="isPlaying"
        >
    </div>
</template>

<script>

export default {
	name: 'controls',
    props: {
        isPlaying: { type: Boolean, default: false},
        finalScore: { type: Number, default: 0},
        isWinner: { type: Boolean, default: false},
    },
	data () {
		return {
		}
	},
    methods: {
        rollDice() {
            this.$emit('rollDice');
        },
        initNewGame() {
            this.isPopUpOpen = true;
            this.$emit('initNewGame');
        },
        holdScore() {
            this.$emit('holdScore');
        },
    }
}
</script>

<style scoped>
    .control {
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
        width: 200px;
        background: none;
        border: none;
        font-family: Lato;
        font-size: 20px;
        color: #42b983;
        text-transform: uppercase;
        cursor: pointer;
        font-weight: 300;
        transition: all 0.3s, color 0.3s;
        letter-spacing: 0px;
    
    }
    .control:hover {
        color: #3e6956;
        letter-spacing: 2px;
    }
    .new-game-btn {
        top: 35px
    }
    .roll-dice-btn {
        top: 400px;
    }
    .hold-btn {
        top: 450px;
    }
    .final-score {
        top: 500px;
        text-align: center;
        font-weight: 500;
        color: black;
        font-weight: bold;
    }
</style>