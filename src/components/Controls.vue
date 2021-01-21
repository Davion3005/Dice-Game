<template lang="pug">
    div.wrapper-controls
        button.control.btn-new( @click="startNewGame")
            i.ion-ios-plus-outline
            | New game
        button.control.btn-roll(@click="rollDices")
            i.ion-ios-loop
            | Roll dice
        button.control.btn-hold
            i.ion-ios-download-outline
            | Hold
        input.final-score(type='number' placeholder='Final score')
</template>

<script>
    export default {
        name: "controls",
        data() {
            return {

            }
        },
        methods: {
            startNewGame() {
                this.$emit('newGame')
            },
            rollDices() {
                this.$emit('rollDices')
            }
        },
    }
</script>

<style scoped>
    .control {
        position: absolute;
        width: 200px;
        left: 50%;
        transform: translateX(-50%);
        color: #555;
        background: none;
        border: none;
        font-family: Lato;
        font-size: 20px;
        text-transform: uppercase;
        cursor: pointer;
        font-weight: 300;
        transition: background-color 0.3s, color 0.3s;
    }
    .control.disable {
        pointer-events: none;
    }

    .control:hover { font-weight: 600; }
    .control:hover i { margin-right: 20px; }

    .control:focus {
        outline: none;
    }

    .control i {
        color: #42b983;
        display: inline-block;
        margin-right: 15px;
        font-size: 32px;
        line-height: 1;
        vertical-align: text-top;
        margin-top: -4px;
        transition: margin 0.3s;
    }

    .btn-new { top: 45px;}
    .btn-roll { top: 403px;}
    .btn-hold { top: 467px;}

    .final-score {
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
        top: 520px;
        color: #555;
        font-size: 18px;
        font-family: 'Lato';
        text-align: center;
        padding: 10px;
        width: 160px;
        text-transform: uppercase;
    }

    .final-score:focus { outline: none; }
</style>
