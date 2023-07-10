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
                v-bind:isPlaying="isPlaying"
                v-bind:finalScore="finalScore"
                v-on:rollDice="rollDice"
                v-on:initNewGame="initNewGame"
                v-on:holdScore="holdScore"
                v-on:changeFinalScore="changeFinalScore"
                v-bind:isWinner="isWinner"

            />
            <dices 
                v-bind:dices="dices"
            />
            <popUp 
                v-bind:isPopUpOpen="isPopUpOpen"
                v-on:confirmToPlay="confirmToPlay"
            />
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
            finalScore: null,
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
            if (this.isPlaying && !this.isWinner) {
                if (dice1 === 1 || dice2 === 1) {
                    let activePlayer = this.activePlayer;
                    setTimeout(function() {
                        alert(`Player ${activePlayer + 1} has got dice number 1. How unfortunate!`)
                    }, 500)
                    this.nextPlayer();
                } else {
                    this.currentScore = this.currentScore + dice1 + dice2;
                }
                
            } else {
                alert('Please click the new game button');
            }
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
            this.activePlayer = this.activePlayer === 0 ? 1 : 0;
            this.currentScore = 0;
        },
        holdScore() {
            if (this.isPlaying) {
                let { currentScore, activePlayer, playerScores } = this;
                let oldSCore = playerScores[activePlayer];                
                this.$set(this.playerScores, activePlayer, oldSCore + currentScore);
                if (!this.isWinner) {
                    this.nextPlayer();
                }

            } else {
                alert('Please click the new game button');
            }
        }
    },
    computed: {
        isWinner() {
            let { finalScore, playerScores } = this;
            console.log('calculating fs');
            
            if (this.isPlaying) {
                console.log('final score', finalScore);
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
