<template>
    <div class="icons">
        <swiper :options="swiperOption">
            <swiper-slide v-for="(page,index) of pages" :key="index">
                <div class="icon" v-for="item of page" :key="item.id" >
                    <div class="icon-img">
                        <img class="icon-imgcontent" :src="item.imgUrl" alt="">
                    </div>
                    <p class="icon-desc">{{item.desc}}</p>
                </div>
            </swiper-slide>
        </swiper>
    </div>
</template>

<script>
export default {
    name:'HomeIcons',
    props:{
        list:Array
    },
    data(){
        return{
            swiperOption:{
                // pagination: ".swiper-pagination",
                loop: false
            },
        }
    },
    methods:{

    },
    computed:{
        pages(){
            const pages = [];
            this.list.forEach((item,index)=>{
                const page = Math.floor(index/8);
                if(!pages[page]){
                    pages[page] = [];
                }
                pages[page].push(item)
            })
            return pages
        } 
    }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl';
@import '~styles/mixins.styl';
.icons >>> .swiper-container
    // height 0
    // padding-bottom 50%
.icons 
    padding-top 10px
    .icon
        position relative
        overflow hidden
        width 25%
        height 160px
        padding-top 5px
        float left
        display flex
        flex-direction column
        align-items center
        .icon-img 
            height 110px
            width 110px
            .icon-imgcontent
                display block
                height 100%
                margin 0 auto 
        .icon-desc
            text-align center
            width 188px 
            height 44px
            font-size 28px
            color $darkTextColor
            ellipsis()
        
</style>
