<template lang="pug">
    #app
        .wrapper.clearfix
            players(:playerScores="playerScores" :currentScore="currentScore" :isPlayingPlayer="isPlayingPlayer")
            controls(@newGame="handleNewGame"
                @rollDices="handleRollDices"
                @holdScore="handleHoldScore"
                @changeFinalScore="handleChangeFinalScore"
                :finalScore="finalScore"
                :isPlaying="isPlaying")
            dices(:diceFaces="diceFaces")
            game-rule(:isOpenPopup="isOpenPopup" @agreeRule="handleAgreeRule")
</template>

<script>
import Players from "@/components/Players";
import Controls from "@/components/Controls";
import Dices from "@/components/Dices";
import {PLAYER} from "@/app/config/others";
import GameRule from "@/components/GameRule";

export default {
    name: 'App',
    components: {
        GameRule,
        Dices,
        Controls,
        Players,
    },
    data() {
        return {
            isPlaying: false,
            isPlayingPlayer: PLAYER.player1,
            playerScores: [0, 0],
            currentScore: 0,
            isOpenPopup: false,
            diceFaces: [1,1],
            finalScore: 100,
        }
    },
    methods: {
        handleNewGame() {
            this.isOpenPopup = true
        },
        handleAgreeRule() {
            this.isOpenPopup = false;
            this.isPlaying = true;
            this.isPlayingPlayer = PLAYER.player1;
            this.playerScores = [0, 0];
            this.currentScore = 0;
            this.diceFaces = [1, 1];
        },
        handleRollDices() {
            //Check whether already click "NewGame button"
            if (this.isPlaying) {
                //Roll dices
                let dice1Value = Math.ceil(Math.random() * 6);
                let dice2Value = Math.ceil(Math.random() * 6);
                this.diceFaces = [dice1Value, dice2Value];

                //Check if any dice is 1
                if (dice1Value === 1 || dice2Value === 1) {
                    let playerName = this.isPlayingPlayer + 1;
                    setTimeout(function () {
                        alert('Player '  + playerName + ' has been lost turn!');
                    }, 50);
                    console.log('Should not stop here in first roll')
                    this.changeTurn();
                } else {
                    this.currentScore = this.currentScore + dice1Value + dice2Value;
                }

            } else {
                alert('Please click button New Game')
            }
        },
        changeTurn() {
            this.isPlayingPlayer = this.isPlayingPlayer === PLAYER.player1 ? PLAYER.player2 : PLAYER.player1;
            this.currentScore = 0;

        },
        handleHoldScore() {
            if (this.isPlaying) {
                if (this.currentScore >= 2) {
                    let {playerScores, isPlayingPlayer, currentScore} = this;

                    let clonePlayerScores = [...playerScores];
                    clonePlayerScores[isPlayingPlayer] = clonePlayerScores[isPlayingPlayer] + currentScore;
                    this.playerScores = [...clonePlayerScores];
                    this.changeTurn();
                } else {
                    alert('Please roll dice at least 1 time');
                }
            } else {
                alert('Please click button New Game');
            }
        },
        handleChangeFinalScore(e) {
            this.finalScore = isNaN(parseInt(e.target.value)) ? "" : parseInt(e.target.value);
        },
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
        background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url(assets/back.jpg);
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
    }
</style>
