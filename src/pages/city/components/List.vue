<template>
    <div class="list" ref="wrapper">
        <div>
            <div class="area">
                <div class="title border-topbottom">当前城市</div>
                <div class="button-list">
                    <div class="button-wrapper">
                        <div class="button">{{this.$store.state.city}}</div>
                    </div>
                </div>
            </div>
            <!-- 热门城市star -->
            <div class="area">
                <div class="title border-topbottom">热门城市</div>
                <div class="button-list">
                    <div class="button-wrapper" 
                        v-for="item in hotCities" 
                        :key="item.id"
                        @click="handleCityClick(item.name)"
                    >
                        <div class="button">{{item.name}}</div>
                    </div>
                </div>
            </div>
            <!-- 热门城市end -->
            <div class="area" 
                v-for="(item,key) of cities" 
                :key="key"
                :ref="key"
            > 
                <div class="title border-topbottom">{{key}}</div>
                <div class="item-list">
                    <div class="item border-bottom" 
                        v-for="innerItem of item" 
                        :key="innerItem.id"
                        @click="handleCityClick(innerItem.name)"
                    >
                    {{innerItem.name}}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Bscroll from 'better-scroll'
export default {
    name:'CityList',
    props:{
        hotCities:Array,
        cities:Object,
        letter:String
    },
    methods:{
        handleCityClick(city){
            this.$store.dispatch('changeCity',city)
            this.$router.push('/')
        }
    },

    watch:{
        letter(){
            if(this.letter){
                const element = this.$refs[this.letter][0]
                console.log(element)
                this.scroll.scrollToElement(element)
            }
            console.log(this.letter)
        }
    },
    mounted(){
        this.scroll = new Bscroll(this.$refs.wrapper)//引用better-scroll
    },
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl';
.border-topbottom
    &:before
        border-color #ccc
    &:after
        border-color #ccc
    
.border-bottom
    &:before
        border-color #ccc
.list
    position absolute
    overflow hidden
    top 168px
    left 0
    right 0
    bottom 0
    .title
        line-height 54px
        background #eee
        padding-left 20px
        color #666
        font-size 26px
    .button-list
        padding 10px 60px 10px 10px
        overflow hidden
        .button-wrapper
            float left
            width 33.33%
            .button
                margin 10px
                text-align center
                border-radius 6px
                border 2px solid #cccccc
                padding 10px 0
                font-size 28px

    .item-list
        .item
            line-height 54px
            padding 20px
</style>
