<template>
	<div id="app">
        <div class="wrapper clearfix">
            <players
                v-bind:currentScore="currentScore"
                v-bind:playerScores="playerScores"
                v-bind:activePlayer="activePlayer"
                v-bind:isWinner="isWinner"
            />
            <controls 
                v-on:rollDice="rollDice"
                v-on:initNewGame="initNewGame"
                v-bind:finalScore="finalScore"

            />
            <dices 
                v-bind:dices="dices"
            />
        </div>
	</div>
</template>

<script>
import Players from './components/Players';
import Controls from './components/Controls';
import Dices from './components/Dices';
// import PopupRule from './components/PopupRule';

export default {
	name: 'app',
	data () {
		return {
            isPlaying: false,
            activePlayer: 0,
            dices: [2, 2],
            currentScore: 0,
            playerScores: [0, 0],
            finalScore: 10,
		}
	},

    components: { 
        Players,
        Controls,
        Dices
    },

    methods: {
        initNewGame() {
            console.log(this);
            this.currentScore = 0;
            this.dices = [2, 2];
            this.finalScore = 0;
        },
        rollDice() {
            // 0 <= dice <= 6 =>
            var dice1 = Math.floor(Math.random() * 6) + 1;
            var dice2 = Math.floor(Math.random() * 6) + 1;

            this.dices = [dice1, dice2];
        },
        changeFinalScore(e) {
            var number = parseInt(e.target.value);
            if (isNaN(number)) {
                this.finalScore = '';
            } else {
                this.finalScore = number;
            }
        }
    },
    computed: {
        getPlayerScore() {

        },
        isWinner() {
            let { finalScore, playerScores } = this;
            if (playerScores[0] >= finalScore || playerScores[1] >= finalScore) {
                this.isPlaying = false;
                return true;
            }
            return false;
        }
    }

}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('/public/assets/bg2.jpg');
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
    border-radius: 20px;
}
</style>
