<template>
    <div class="controls">
        <button 
            v-on:click="newGame"
            class="control btn-new"
        ><i class="ion-ios-plus-outline"></i>{{ titleStatus }}</button>
        
        <button 
            v-on:click="rollDice"
            class="control btn-roll"
        ><i class="ion-ios-loop"></i>Lắc xí ngầu</button>

        <button
            v-on:click="holdScore"
            class="control btn-hold"
        ><i class="ion-ios-download-outline"></i>Giữ điểm</button>
        <input
            v-bind:disabled="activeFinalScore"
            v-bind:value="finalScore"
            v-on:input="$emit('handleFinalScore', $event)"
        type="number" placeholder="Final score" class="final-score">
    </div>
</template>

<script>
export default {
    name: 'Controls',
    props: {
        finalScore: {type:[Number, String], default:0},
        activeFinalScore: {type: Boolean, default: false},
        titleStatus: {type: String, default: 'Chơi mới'}
    },
    data() {
        return {
            
        }
    },
    methods: {
        newGame() {
            // console.log('newGame')
            this.$emit('handleNewGame')
        },
        rollDice() {
            this.$emit('handleRollDice')
        },
        holdScore() {
            this.$emit('handleHoldScore')
        }
    }
}
</script>

<style>
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