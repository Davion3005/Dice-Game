<template lang="pug">
    #app
        .wrapper.clearfix
            players(:playerScores="playerScores" :currentScore="currentScore" :isPlayingPlayer="isPlayingPlayer")
            controls
            dices
</template>

<script>
import Players from "@/components/Players";
import Controls from "@/components/Controls";
import Dices from "@/components/Dices";
import {PLAYER} from "@/app/config/others";

export default {
    name: 'App',
    components: {
        Dices,
        Controls,
        Players,
    },
    data() {
        return {
            isPlaying: false,
            isPlayingPlayer: PLAYER.player1,
            playerScores: [12, 20],
            currentScore: 11,
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
