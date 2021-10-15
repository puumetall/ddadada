<template>
    <section>
        <img src='../assets/donkey.jpg'  v-if='showImage' class="donkeys" @click="hide"/>
        <audio ref="audioElm" src="../assets/kaching.mp3"></audio>
        <audio ref="ohno" src="../assets/shdonkey.mp3"></audio>
        <button class="button is-warning" @click="autoClick" :disabled="clicks<cost" style="background_color:red"> {{name}} ({{cps}} clicks per second) cost: {{cost}} clicks
        </button>
    </section>
</template>

<script>
export default {
    data: {
        showImage: true,
    },
    props: ['cost', 'cps', 'name', 'clicks', 'index'],
    methods: {
        autoClick(){
            this.$emit('clicked', this.index);
            this.$refs.audioElm.play(); 
            this.showImage = !this.showImage;
        },
        hide(){
            this.showImage = false;
            this.$refs.ohno.play(); 

        }
    }
}
</script>

<style>
 .donkeys {
     position: fixed;
     top: 60%;
     height: 100px;
     width: auto;
     border-radius: 200px;
 }
 .button.is_warning{
     background-color: red;
 }
</style>