<template lang="pug">
    div.wrapper-players
        .player-panel(:class="getPlayerClass(0)")
            .player-name {{ getPlayerName(0) }}
            .player-score {{ playerScores[0] }}
            .player-current-box
                .player-current-label Current
                .player-current-score {{ isPlayingPlayer === player1 ? currentScore : 0}}
        .player-panel(:class="getPlayerClass(1)")
            .player-name {{ getPlayerName(1) }}
            .player-score {{ playerScores[1] }}
            .player-current-box
                .player-current-label Current
                .player-current-score {{ isPlayingPlayer === player2 ? currentScore : 0 }}
</template>

<script>
import {PLAYER} from "@/app/config/others";
export default {
    name: "players",
    props: {
        playerScores: {
            type: Array,
            default: () => [0, 0]
        },
        currentScore: {
            type: Number,
            default: 0,
        },
        isPlayingPlayer: {
            type: Number,
            default: 0,
        },
        isWinner: {
            type: Boolean,
            default: false,
        },
    },
    data() {
        return {
            player1: PLAYER.player1,
            player2: PLAYER.player2,
        }
    },
    methods: {
        getPlayerName(index) {
            let playerName = 'Player ' + (index + 1);
            if (this.isWinner && (index) === this.isPlayingPlayer) {
                playerName = 'WINNER';
            }
            return playerName;
        },
        getPlayerClass(index) {
            if (!this.isWinner) {
                return {active: this.isPlayingPlayer === index}
            } else {
                return {winner: this.isPlayingPlayer === index}
            }
        },
    },
}
</script>

<style scoped>

    .player-panel {
        width: 50%;
        float: left;
        height: 600px;
        padding: 100px;
        transition: all .3s ease;
        background-color: #fff;
    }
    .player-name {
        font-size: 40px;
        text-align: center;
        text-transform: uppercase;
        letter-spacing: 2px;
        font-weight: 100;
        margin-top: 20px;
        margin-bottom: 10px;
        position: relative;
    }

    .player-score {
        text-align: center;
        font-size: 80px;
        font-weight: 100;
        color: #42b983;
        margin-bottom: 130px;
    }

    .active { background-color: #f7f7f7; }
    .active .player-name { font-weight: 300; }

    .active .player-name::after {
        content: "\2022";
        font-size: 47px;
        position: absolute;
        color: #42b983;
        top: -7px;
        right: 10px;

    }

    .player-current-box {
        background-color: #42b983;
        color: #fff;
        width: 40%;
        margin: 0 auto;
        padding: 12px;
        text-align: center;
    }

    .player-current-label {
        text-transform: uppercase;
        margin-bottom: 10px;
        font-size: 12px;
        color: #222;
    }

    .player-current-score {
        font-size: 30px;
    }

    .winner { background-color: lightblue; }
    .winner .player-name { font-weight: 300; color: #42b983; }
</style>
