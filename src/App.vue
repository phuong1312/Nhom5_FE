<template>
	<div id="app">
		<div class="wrapper clearfix">    
			<!-- Props chuyen du lieu tu cha sang con
                 v-bind rang buoc du lieu (html)
                    1 chieu tu data -> input
                 v-model rang buoc du lieu 2 chieu
                    1 chieu tu data -> input
                    1 chieu tu input -> data-->
			<players 
            v-bind:isWinner="isWinner"
            v-bind:scorePlayer="scorePlayer"
            v-bind:activePlayer="activePlayer"
            v-bind:currentScore="currentScore"/>
			<controls 
            v-bind:isPlaying="isPlaying"
            v-bind:finalScore="finalScore"
            v-on:handleChangeFinalScore="handleChangeFinalScore"
            v-on:handleNewGame="handleNewGame"
            v-on:handleRollDice="handleRollDice"
            v-on:handleHoldCore="handleHoldCore"/>
            <dices 
            v-bind:dices="dices"/>
            <popup-rule 
            v-on:handleConfirm="handleConfirm"
            v-bind:isOpenPopup="isOpenPopup"/>
        </div>
	</div>
</template>

<script>
import Players from './components/Players.vue'
import Controls from './components/Controls.vue'
import Dices from './components/Dices.vue'
import PopupRule from './components/PopupRule.vue'
export default {
	name: 'app',
	data () {
		return {
            activePlayer: 0, // active player: luu nguoi choi hien tai
			scorePlayer: [0, 0],
            currentScore: 0,
            dices: [1, 6], 
            isPlaying: false,
            isOpenPopup: false,
            finalScore: "",
		}
	},
	components: {
		Players,
		Controls,
		Dices,
        PopupRule
	},
    computed: {
        isWinner() {
            let {scorePlayer, finalScore} = this;

            if (scorePlayer[0] >= finalScore || scorePlayer[1] >= finalScore) {
                //Dung cuoc choi
                this.isPlaying = false;
                return true;
            }
            return false;
        }
    },
    methods: {
        handleChangeFinalScore(e) {
            var number = parseInt(e.target.value);
            if (isNaN(number)) {
                this.finalScore = '';
            } else {
                this.finalScore = number;
            }
        },
        handleHoldCore() {
            if (this.isPlaying ) {
                let {scorePlayer, activePlayer, currentScore} = this;
                let scoreOld = scorePlayer[activePlayer];
                let cloneScore = [...scorePlayer];
                cloneScore[activePlayer] = scoreOld + currentScore;
                this.scorePlayer = cloneScore;
                console.log(this.scorePlayer);
                // this.$set(this.scorePlayer, activePlayer, scoreOld + currentScore);
                if (!this.isWinner) {
                    this.nextPlayer();
                }
            } else {
                alert('Vui lòng nhấp vào nút Bắt Đầu để bắt đầu cuộc chơi');
            }
            // console.log("Hold Core");
        },
        nextPlayer() {
            //active player = 0 thi doi ve 1 va nguoc lai
            this.activePlayer = this.activePlayer === 0 ? 1 : 0
            this.currentScore = 0;
        },
        handleConfirm() {
            // console.log("handleConfirm PopupRule.vue");
            this.isPlaying = true;
            this.isOpenPopup = false;
            this.activePlayer = 0;
            this.dices = [1, 1];
            this.scorePlayer = [0, 0];
            this.currentScore = 0;
        },
        handleNewGame() {
            // console.log ('handleNewGame App.vue');
            if (this.finalScore == 0 || this.finalScore == "") {
                alert('Vui lòng nhập điểm cuối cùng để bắt đầu');
            } else {
                this.isOpenPopup = true;
            }
        },
        handleRollDice() {
            // console.log ('handleRollDice App.vue');
            if (this.isPlaying) {
                //Xoay xuc xac
                //Math.random() chi so le
                var dice1 = Math.floor(Math.random() * 6) + 1;
                var dice2 = Math.floor(Math.random() * 6) + 1;

                this.dices = [dice1, dice2];
                console.log (dice1, dice2);

                if (dice1 === 1 || dice2 === 1) {
                    let activePlayer = this.activePlayer + 1;
                    //Doi luot choi
                    setTimeout(function() {
                        alert('Người chơi đã quay trúng số 1');
                    },10)
                    this.nextPlayer();
                    //Reset diem ve 0
                } else {
                    //Cong don vao diem hien tai
                    this.currentScore = this.currentScore + dice1 + dice2;
                }
            } else {
                alert('Vui lòng nhấp vào nút Bắt Đầu để bắt đầu cuộc chơi');
            }
        }
    }
}
</script>

<style >
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
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url(../public/images/back.jpg);
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
