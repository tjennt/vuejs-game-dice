<template>
  <div id="app" class="wrapper clearfix">
    <players
      v-bind:scoresPlayer="scoresPlayer"
      v-bind:activePlayer="activePlayer"
      v-bind:currentScore="currentScore"
      v-bind:checkWinner="checkWinner"
    />
    
    <controls 
      v-on:handleNewGame="handleNewGame"
      v-on:handleRollDice="handleRollDice"
      v-on:handleHoldScore="handleHoldScore"

      v-bind:finalScore="finalScore"
      v-on:handleFinalScore="handleFinalScore"

      v-bind:activeFinalScore="activeFinalScore"

      v-bind:titleStatus="titleStatus"
    />
    
    <dices 
      v-bind:dices="dices"
    />

    {{ finalScore }}
    <popup-rule 
      v-bind:isOpenPopup="isOpenPopup"
      v-on:handleConfirm="handleConfirm"
    />
  </div>
</template>

<script>
import Players from './components/Players'
import Controls from './components/Controls'
import Dices from './components/Dices'
import PopupRule from './components/PopupRule'

export default {
  name: 'App',
  components: {
    Players,
    Controls,
    Dices,
    PopupRule
  },
  data() {
    return {
      isPlaying: false,
      isOpenPopup: false,
      scoresPlayer: [23,33],
      dices: [4,2],
      currentScore: 43,
      activePlayer: 2,
      finalScore: 30,
      activeFinalScore: false,
      titleStatus: 'Chơi mới',
      checkWinner: 2
    }
  },
  methods: {
    handleFinalScore(e) {
      // console.log(e.target.value)
      let number = parseInt(e.target.value)
      if(isNaN(number)){
        this.finalScore = ''
      }else{
        if(number <= 0 ){
          number = 1
        }
        this.finalScore = number
      }
    },
    handleNewGame() {
      // console.log('handleNewGame')
      this.isOpenPopup = true
    },
    handleConfirm() {
      this.isPlaying = true
      this.isOpenPopup = false
      this.scoresPlayer = [0,0]
      this.dices = [1,1]
      this.currentScore = 0
      this.activePlayer = Math.floor(Math.random() * 2)
      this.activeFinalScore = true
      this.titleStatus = "Chơi lại"
      this.checkWinner = 2
      // console.log('handleConfirm')
    },
    nextPlayer() {
      this.currentScore = 0
      this.activePlayer = this.activePlayer === 1 ? 0 : 1
    },
    handleRollDice() {
      if(this.isPlaying){
        // console.log('handleRollDice')
        let dice1 = Math.floor(Math.random() * 6) + 1
        let dice2 = Math.floor(Math.random() * 6) + 1

        this.dices = [dice1, dice2]
        // console.log({dice1, dice2})
        if(dice1 === 1 || dice2 === 1){
          // END GAME
          this.nextPlayer()
        }else{
          this.currentScore += dice1 + dice2
        }
      }else{
        alert('Vui lòng chọn chơi mới')
      }
    },
    handleHoldScore() {
      if(this.isPlaying && this.currentScore !== 0){
        this.scoresPlayer[this.activePlayer] += this.currentScore
        if(this.scoresPlayer[0] >= this.finalScore || this.scoresPlayer[1] >= this.finalScore){
          this.handleWinner(this.activePlayer)
        }else{
          this.nextPlayer()
        }
      }else{
        if(!this.isPlaying){
          alert('Vui lòng chọn chơi mới')
        }
      }
    },
    handleWinner(activePlayer) {
        // console.log('winner')
        this.checkWinner = activePlayer 
        this.isPlaying = false
        this.titleStatus = 'Chơi mới'
        this.activeFinalScore = false
        let playerNumber = parseInt(activePlayer) + 1
        alert('Chúc mừng người chơi thứ '+ playerNumber +' đã chiến thắng')
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
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url("./assets/back.jpg");
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
