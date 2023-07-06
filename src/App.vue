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
            <popUp 
                v-on:confirmToPlay="confirmToPlay"
                v-bind:isPopUpOpen="isPopUpOpen"/>
        </div>
	</div>
</template>

<script>
import Players from './components/Players';
import Controls from './components/Controls';
import Dices from './components/Dices';
import PopUp from './components/PopUp';

export default {
	name: 'app',
	data () {
		return {
            isPlaying: false,
            activePlayer: null,
            dices: [2, 2],
            currentScore: 0,
            playerScores: [0, 0],
            finalScore: 100,
            isPopUpOpen: false
		}
	},

    components: { 
        Players,
        Controls,
        Dices,
        PopUp,
    },

    methods: {
        initNewGame() {
            this.isPopUpOpen = true;
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
        },
        confirmToPlay() {
            this.isPlaying = true;
            this.isPopUpOpen = false;
            this.activePlayer = 0;
            this.dices = [2, 2];
            this.playerScores = [0, 0];
            this.currentScore = 0;
        },
        nextPlayer() {
            if (this.activePlayer === 0) {
                this.activePlayer === 1 
            } else {
                this.activePlayer === 0;
            }
        },
        holdScore() {
            console.log('ok');
            if (this.isPlaying && !this.isWinner) {
                let { currentScore, activePlayer, playerScores, dices } = this;
                playerScores[activePlayer] = dices[0] + dices[1];
                currentScore += playerScores[activePlayer];
    
                if (dices[0] === 1 || dices[1] === 1) {
                    this.nextPlayer();
                }
            }
        }
    },
    computed: {
        getPlayerScore() {

        },
        isWinner() {
            let { finalScore, playerScores } = this;
            if (this.isPlaying) {
                if (playerScores[0] >= finalScore || playerScores[1] >= finalScore) {
                    this.isPlaying = false;
                    return true;
                }
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
    border-radius: 10px;
}
</style>
