<template>
<div id="app">
   <div class="wrapper clearfix">
            <players
            :scorePlayer = "scorePlayer"
            :currentScore = "currentScore"
            :activePlayer = "activePlayer"

            />
            <controls
            :finalScore = "finalScore"
            @handleEvent="handleEventnewgame"
            @rolldicetoApp = "rolldiceonApp"
            @handleHoldscore = "handleHoldscoreApp"
            @handleFinalScore = "handleFinalScoreApp"
            />
            <dices
            :dices = "dices"            
            />
            <popup-rule
            :isOpenPopup = "isOpenPopup"
            @confirmpopup = "confirmpopuponApp"
            />
    </div>
 </div>
</template>

<script>
import Players from "@/components/Players";
import Controls from "@/components/Controls";
import Dices from "@/components/Dices";
import PopupRule from "@/components/PopupRule";

export default {
  name: 'app',
  data: function(){
    return {
        isPlaying: false,
        activePlayer: 1,
        isOpenPopup: false,
        scorePlayer: [10, 11],
        currentScore: 50,
        dices: [1, 6],
        finalScore: 100

      }
  },
  components: {
   Players,
   Controls,
   Dices,
   PopupRule
  },

  methods: {

    handleFinalScoreApp(e){
      console.log(e.target.value + " " + parseInt(e.target.value));
    },

    handleHoldscoreApp: function(){

      if(this.isPlaying){
        // Destructure object
        let {scorePlayer, activePlayer, currentScore} = this;

        let scoreOld = scorePlayer[activePlayer];

        // Another method to clone array using spread operator: let a = [...b], $set is Vue method

        this.$set(this.scorePlayer, activePlayer, scoreOld + currentScore);

        this.nextPlayer();

      }else{

        alert ("Please click on the New game button first");

      }
    },

    handleEventnewgame: function(){
      this.isOpenPopup = true;
      console.log("From app.vue")
    },
    confirmpopuponApp: function(){      
      this.isOpenPopup = false;
      this.isPlaying = true;
      this.activePlayer = 0;
      this.scorePlayer = [0, 0];
      this.currentScore = 0;
      this.dices = [1, 1]

      console.log("Receive emit event from PopupRule.vue. Agree with the rule :-)");
    },

    nextPlayer: function(){
      this.activePlayer = this.activePlayer === 0 ? 1: 0;

      this.currentScore = 0;

    },

    rolldiceonApp: function(){

      console.log("Received the rolldice event");

      if(this.isPlaying){

          let dice1 = Math.floor(Math.random() * 6) + 1;

          let dice2 = Math.floor(Math.random() * 6) + 1;

          this.dices = [dice1, dice2];

          if(dice1 === 1 || dice2 === 1){
   
            setTimeout(()=>{
                alert(`The player ${this.activePlayer} sadly get 1 in one of your dices, then you fail! Sorry`)
            }, 10)
            
            this.nextPlayer();

          }else{
            this.currentScore = this.currentScore + dice1 + dice2;
          }

          console.log(dice1, dice2);

      }else{
        alert("You need to click on the new game first")
      }
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
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url("assets/back.jpg");
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
