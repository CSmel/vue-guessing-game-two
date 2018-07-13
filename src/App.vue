<template>
    <div id="app">
        <div class="container">
            <label>YOU</label>
            <div id="card">

                <input class="card-num-cont" v-model="playerNum">

            </div>
            <div class="display-content">

                <img class="gif-container" v-bind:src="determin"></div>
            <div id="card-guess">

                <div class="card-guess-cont">{{computerNum}}</div>
            </div>
            <label>ROBOT</label>
            <button v-if="start" @click="randomNum">Lets Play!</button>
            <button v-if="replay" @click="resetButton">Again?!</button>
        </div>

    </div>
</template>

<script>
    export default {
        name: 'app',
        data() {
            return {
                playerNum: '',
                computerNum: '',
                //winner: 'WON',
                //loser: 'Lost',
                //surprise:'https://media.giphy.com/media/x4O0fjpQfoBZS/giphy.gif',
                resetVal: '',
                start: true,
                replay: false,
            }
        },

        methods: {
            randomNum: function () {

                if (this.playerNum > 0 && this.playerNum < 11) {
                    this.computerNum = Math.floor(Math.random() * (11 - 1)) + 1;
                    return [this.computerNum, this.playButton()];
                }

                else {
                    return this.resetVal;
                }

            },
            playButton: function () {
                if (this.start === true || this.replay === false) {
                    return [this.start = false, this.replay = true]
                }
            },

            resetButton: function () {

                if (this.computerNum !== this.playerNum && this.start === false && this.replay === true)

                    return [this.computerNum = '', this.playerNum = '', this.start = true, this.replay = false];
            }
        },

        computed: {
            determin: function () {
                if (this.playerNum === '0' || this.playerNum < 0) {
                    return 'https://media.giphy.com/media/3og0IJXQEKwIdIEYpy/giphy.gif';//try again
                }
                else if (this.computerNum === '' || this.playerNum === '') {
                    return 'https://media.giphy.com/media/zaezT79s3Ng7C/giphy.gif'; //start
                }
                else if (this.computerNum == this.playerNum) {
                    return 'https://media.giphy.com/media/x4O0fjpQfoBZS/giphy.gif'; //balloon
                }
                else if (this.computerNum !== this.playerNum) {
                    return 'https://media.giphy.com/media/d2W7eZX5z62ziqdi/giphy.gif'; //fail
                }


            },

        },
    }
</script>

<style>

    @import url("https://fonts.googleapis.com/css?family=BioRhyme+Expanded|Song+Myung");

    /*===============================
    small phones @ 320px width
    ================================*/

    #card {
        margin: 0 auto;
    }

    #card-guess {
        margin: 0 auto;
    }

    .container {
        display: flex;
        margin: 0 auto;
        align-content: center;
        align-items: center;
        flex-direction: column;
        height: 80vh;
        width: 100%;
        background-color: cadetblue;
    }

    .card-guess-cont, .card-num-cont {
        font-family: 'BioRhyme Expanded', serif;
        font-size: 1.5em;
        text-align: center;
        line-height: 50px;
        height: 50px;
        width: 50px;
        background-color: #fff;
        margin: 5px;
    }

    button {
        margin-top: 10px;
        border: 1px solid #000;
        width: 100px;
        height: 50px;

        font-family: 'BioRhyme Expanded', serif;
        border-top-right-radius: 10px;
        border-top-left-radius: 10px;
        border-bottom-right-radius: 10px;
        border-bottom-left-radius: 10px;
    }

    input {
        border: none;
    }

    label {
        font-weight: bolder
    }

    .display-content {
        display: flex;
        align-items: center;
        align-content: center;
        width: 80vw;
        height: 100vh;
    }

    .gif-container {
        width: auto;
        height: 20vh;
        margin: auto;
        border: none !important;
    }

    @media (min-width: 768px) {
        .container {
            flex-direction: row;
        }

        .gif-container {
            width: auto;
            height: 40vh;
            margin: auto;
            border: none !important;
        }

        button {
            background-color: cadetblue;
            top: 70%;
            left: 50%;
            position: absolute;
            transform: translate(-50%, -50%);
        }

    }
</style>
