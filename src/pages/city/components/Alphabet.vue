<template>
    <ul class="list" >
        <li class="item" 
            v-for="item of letters" 
            :key="item"
            :ref="item"
            @touchstart='handleTouchStart'
            @touchmove='handleTouchMove'
            @touchend='handleTouchEnd'
            @click="handleLetterClick"
        >{{item}}</li>
    </ul>
</template>

<script>
export default {
    props:{
        cities:Object
    },
    data(){
        return{
            touchStatus:false,
            startY:0,
            timmer:null
        }
    },
    updated(){
        this.startY = this.$refs['A'][0].offsetTop
    },
    computed:{
        letters(){
            const letters = []
            for(let i in this.cities){
                letters.push(i)
            }
            return letters
        }
    },
    methods:{
        handleLetterClick(e){
            this.$emit('change',e.target.innerText)
            console.log(e.target.innerText)
        },
        handleTouchStart(){
            this.touchStatus = true;
        },
        handleTouchMove(e){
            if(this.touchStatus){
                if(this.timmer){
                    clearTimeout(this.timmer)
                }
                this.timmer = setTimeout(() => {
                    // const startY = this.$refs['A'][0].offsetTop
                    const touchY = e.touches[0].clientY - 79
                    const index = Math.floor((touchY - this.startY)/20)
                    if(index>=0&&index<this.letters.length){
                        this.$emit('change',this.letters[index])
                    }
                    console.log(touchY)
                    console.log(index)
                }, 16);

            }
        },
        handleTouchEnd(){
            this.touchStatus = false;
        },
    }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl';
.list
    display flex
    flex-direction column
    justify-content center
    position absolute
    right 0
    top 250px
    bottom 0
    width 40px
    .item
        line-height 45px
        text-align center
        color $bgColor
</style>
