<template>
  <section class="section">
        <button class="question" @click="getcoins" >Answer this, get rich</button>
        <meta charset=“UTF-8”>
        <audio ref="incorrect" src="../assets/incorrect.mp3"></audio>
        <audio ref="correct" src="../assets/correct.mp3"></audio>
        <audio ref="freeze" src="../assets/nioce.mp3"></audio>
        <audio ref="shrek" src="../assets/shrek.mp3"></audio>
        <img src="../assets/face.png" alt="shrek" @click="clicks++;sound()" class="shrekbutton">
        <h4 class="clicks">You have {{displayClicks}} clicks!</h4> 
        <button :disabled="disabled" @click="delay" class="free">Free Clicks</button> 
        <button :disabled="disabled" @click="time" class="time">tIME bOMB</button> 
        <div class="costs">
        <auto-click class = "hind" 
        v-for="(auto,index) in autoClickers"
        :key="index"
        :name="auto.name"
        :cps="auto.cps"
        :cost="auto.cost"
        :index="index"
        :clicks="clicks"
        @clicked="autoClick" >
        </auto-click>
        </div>
  </section>
</template>

<script>
import AutoClick from './AutoClick.vue';
export default {
  components: { AutoClick },
    mounted(){
        setInterval(()=>{
            this.clicks += this.cps;   
        },1000);
    },
    data(){
        return {
            clicks: 0,
            cps: 0,
            cost: 10,
            autoClickers: [
                {name: '👌 Auto Click', cost: 10, cps:0.1},
                {name: '🐴 Donkey', cost: 100, cps:1},
                {name: '🐈 Puss', cost: 1000, cps:10},
                {name: '🐉 Dragon', cost: 10000, cps:100},
                {name: '💃 Fiona', cost: 100000000, cps:100000},
            ]
        }
    },
    methods: {
        getcoins(){
            var que = prompt("How many moni");
            if(que=="meni") {
                this.clicks = this.clicks + 10000;
                this.$refs.correct.play();
            } else {
                alert("hah luser");
                this.$refs.incorrect.play();
            }
        },
        sound(){
            this.$refs.shrek.play();
        },
        autoClick(index){
           this.clicks -= this.autoClickers[index].cost; 
           this.cps += this.autoClickers[index].cps;
           this.autoClickers[index].cost += Math.ceil(this.autoClickers[index].cost/7);
        },
        delay () {
        this.disabled = true;
        this.$refs.freeze.play();
        this.timeout = setTimeout(() => {
          this.disabled = false
        }, 1000000)

        this.myFunction()
        },
        myFunction () {
            this.clicks = this.clicks + 100;
        },
        time (){
             this.disabled = true;
        } 
    },
    computed: {
        displayClicks(){
            return this.clicks.toFixed(1);
        }
    }
}
</script>

<style>
    html{
        background-color:#242424 !important;
    }
    .time {
        position:fixed;
        left: 90%;
        top: 70%;
    }
    .time:disabled{
        cursor: not-allowed;
    }
    .question{
        position: fixed;
        top: 80%;
        background-color: yellow;
        width: 150px;
        height: auto;
        font-size: 20px;
        border: solid yellow 1px;
        border-radius: 20px;
    }
    .question:hover{
        transform: scale(1.2);
        background-color: rgb(255, 255, 129);
    }
    .shrekbutton {
        height: 300px;
        width: auto;
        border-radius: 300px;
        position: fixed;
        top: 10%;
        left: 42%;
    }
    .costs {
        width: 20%;
        padding-top: 20px;
    }
    .clicks {
        position: fixed;
        top: 44%;
        left: 41%;
        color:greenyellow;
        font-size: 40px !important;
    }
    .costs button {
        font-size: 20px;
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    }
    .shrekbutton:hover {
        transform: scale(1.1);
    }
    .free {
        background-color: lime;
        color: black;
        border: none;
        height: 260px;
        width: 260px;
        border-radius: 260px;
        font-size: 50px;
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
        float: right;
        margin-right: 20px;
    }
    .free:disabled {
        opacity: 50%;
        cursor: not-allowed;
    }
    .free:hover {
        transform: scale(1.3);
    }
    .button.is-warning {
        background-color: #e56029 !important;
        margin-bottom: 15px;
        width: 500px;
        border: solid #e56029 1px ;
        border-radius: 40px;
    }
    .button.is-warning:hover {
        background-color:#f87238 !important;
    }
</style>