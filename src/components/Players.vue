<template>
    <div class="player-wrapper">
        <div class="player-panel"                 
            v-bind:class="{
                active: activePlayer == 0 && !this.isWinner,
                winner: activePlayer == 0 && this.isWinner,
            }">
            <div class="player-name">
                {{ getPlayerName(0) }}
            </div>
            <div class="player-score">{{ playerScores[0] }}</div>
            <div class="player-current-box">
                <div class="player-current-label">Current</div>
                <div class="player-current-score">{{ activePlayer == 0 ? currentScore : 0 }}</div>
            </div>
        </div>
        <div class="player-panel"
            v-bind:class="{
                active: activePlayer == 1 && !this.isWinner,
                winner: activePlayer == 1 && this.isWinner,
            }">
            <div class="player-name">
                {{ getPlayerName(1) }}
            </div>
            <div class="player-score">{{ playerScores[1] }}</div>
            <div class="player-current-box">
                <div class="player-current-label">Current</div>
                <div class="player-current-score">{{ activePlayer == 1 ? currentScore : 0  }}</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
	name: 'players',
    props: {
        currentScore: { type: Number, default: 0},
        activePlayer: { type: Number, default: 0},
        playerScores: { type: Array, default: [0, 0]},
        finalScore: { type: Number, default: 0},
        isWinner: { type: Boolean, default: false},
    },
	data () {
		return {
		}
	},
    methods: {
        getPlayerName(index) {
            var defaultName = 'Player ' + (index + 1);
            var { playerScores, activePlayer, finalScore } = this;
            if (this.activePlayer === index && playerScores[activePlayer] >= finalScore && this.isWinner) {
                defaultName = 'Winner!';
            }
            return defaultName;
        }
    },
}
</script>

<style scoped>
.player-panel {
    float: left;
    width: 50%;
    transition: all .25s ease;
}
.player-panel.active, .player-panel.winner  {
    background-color: rgba(215, 243, 222, 0.5);
}
.player-name {
    font-size: 50px;
    color: #666;
    font-weight: 100;
    text-transform: uppercase;
    margin: 20px 0 70px 0;
    letter-spacing: 2px;
    position: relative;
    text-align: center;
}
.player-score {
    font-size: 80px;
    font-weight: 400;
    text-align: center;
    margin-bottom: 120px;
}
.player-current-box {
    padding: 20px;
    text-align: center;
    background: #42b983;
    width: 25%;
    margin: 0 auto 85px;
    border-radius: 20px;

}
.player-current-label {
    font-size: 16px;
    margin-bottom: 10px;
}
.player-current-score {
    font-size: 30px;
    color: white;
}
.winner .player-name {
    color: #42b983;
    font-weight: 500;
}
</style>
