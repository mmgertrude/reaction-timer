<template>
  <div class="block" v-if="showBlock" @click="stopTimer">click me</div>
</template>

<script>
export default {
    //specify props to be recieved from App.vue
    props: ["delay"],
    data(){
        return{
            showBlock: false,
            timer: null,
            reactionTime: 0
        }
    },
    //use the lifecycle hook mounted()
    mounted(){
        //code in here fires only when Block.vue 
        //is mounted to the DOM
        //start timer after amount of time = delay
        setTimeout(() =>{
            this.showBlock = true
            this.startTimer()
        }, this.delay)
    },
    methods: {
        //start timer when green block appears
        startTimer(){
            this.timer = setInterval(() => {
                this.reactionTime +=10
            },10)
        },
        //Stop timer when green sq is clicked
        stopTimer(){
            clearInterval(this.timer)
            //send back a custom event to App.vue along with some data (reactionTime)
            this.$emit("endOfGame", this.reactionTime)
        }
    }
    /*,
    updated(){ //this hook fires when any data in the component is updated
        //showBlock was updated to true
        console.log("component updated")
    },
    unmounted(){
        console.log("Block.vue unmounted from App.vue template")
    } */

}
</script>

<style>
.block{
    width: 400px;
    border-radius: 20px;
    background: #0faf87;
    color: white; /*for the text*/
    text-align: center;
    padding: 100px 0;
    margin: 40px auto;
}
</style>