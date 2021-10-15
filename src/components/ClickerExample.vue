<template>
  <section class="section">
        <meta charset=“UTF-8”>
        <audio ref="freeze" src="../assets/nioce.mp3"></audio>
        <audio ref="shrek" src="../assets/shrek.mp3"></audio>
        <img src="../assets/face.png" alt="shrek" @click="clicks++;sound()" class="shrekbutton">
        <h4 class="is-size-4">You have {{displayClicks}} clicks!</h4> 
        <button :disabled="disabled" @click="delay" class="free">Free Clicks</button> 
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
    name: 'your name',
    beforeCreate () {
    document.querySelector('body').setAttribute('style', 'background:#B3FEEE')
    },
    beforeDestroy () {
    document.querySelector('body').setAttribute('style', '')
    },
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
        
    },
    computed: {
        displayClicks(){
            return this.clicks.toFixed(1);
        }
    }
}
</script>

<style>
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
    .is-size-4 {
        position: fixed;
        top: 44%;
        left: 44%;
        color:darkgreen;
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
        height: 200px;
        width: 200px;
        border-radius: 200px;
        font-size: 30px;
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
        float: right;
    }
    .free:disabled {
        opacity: 50%;
    }
    .free:hover {
        transform: scale(1.3);
    }
    .button.is-warning[disabled], fieldset[disabled] .button.is-warning{
        background-color:#e56029;
    }
    .button.is-warning {
        background-color: #e56029;
        margin-bottom: 15px;
        width: 500px;
        border: solid #e56029 1px ;
        border-radius: 40px;
    }
    .button.is-warning.hind:hover {
        background-color: #e9845a;
    }
</style>