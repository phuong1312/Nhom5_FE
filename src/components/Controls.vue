<template>
    <div class="wrapper-controll">
        <!-- v-on:click(ten su kien)="newGame"(function xu ly) -->
        <button
        v-on:click="$emit('handleNewGame')"
        class="control btn-new"><i class="ion-ios-plus-outline"></i>Bắt đầu</button>
        <button 
        v-on:click="$emit('handleRollDice')"
        class="control btn-roll"><i class="ion-ios-loop"></i>Đỗ xúc xắc</button>
        <button 
        v-on:click="$emit('handleHoldCore')"
        class="control btn-hold"><i class="ion-ios-download-outline"></i>Lưu</button>
        
        <input 
        v-bind:disabled="isPlaying"
        v-bind:value="finalScore"
        v-on:input="$emit('handleChangeFinalScore', $event)"
        type="number" placeholder="Điểm cuối cùng" class="final-score">            
    </div>
</template>

<script>
    export default {
        name: 'controls',
        props: {
            //type: [Number, String]: 2 dang du lieu
            finalScore: {type: [Number, String], default: ""},
            isPlaying: {type: Boolean, default: false},
        },
        data() {
            return {
            }
        },
        methods: {
            
        },
    }
</script>

<style>

/**********************************************
*** Control
**********************************************/
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
    font-size: 13px;
    font-family: 'Lato';
    text-align: center;
    padding: 10px;
    width: 160px;
    text-transform: uppercase;
}

.final-score:focus { outline: none; }

</style>
