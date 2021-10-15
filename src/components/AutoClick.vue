<template>
    <section>
        <img src='../assets/donkey.jpg'  v-if='showImage' class="donkeys"/>
        <audio ref="audioElm" src="../assets/kaching.mp3"></audio>
        <button class="button is-warning" @click="autoClick" :disabled="clicks<cost"> {{name}} ({{cps}} clicks per second) cost: {{cost}} clicks
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
</style>