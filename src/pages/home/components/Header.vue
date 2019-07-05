<template>
    <div class="header">
        <div class="header-left">
            <div class="iconfont back-icon">&#xe624;</div>
        </div>
        <div class="header-input">
            <span class="iconfont">&#xe632;</span>
            输入城市/景点/游玩主题</div>
        <router-link to='/city'>
            <div class="header-right">{{this.$store.state.city}}
                <span class="iconfont arrow-icon">&#xeb6d;</span>
            </div>
        </router-link>
    </div>
</template>

<script>
export default {
    name: 'HomeHeader',
    // props:{
    //     city:String
    // }
        
}
</script>

<style lang="stylus" scoped>
    @import '~styles/varibles.styl';
    .header
        display flex
        height $headerHeight
        background $bgColor
        color #ffffff
        line-height $headerHeight
        .header-left 
            width 64px
            float left
            .back-icon
                text-align center
                font-size 36px
        .header-right 
            color #fff
            width 124px
            float right
            margin-left  20px
            font-size 28px
            .arrow-icon
                font-size 24px
                margin-left  -4px
        .header-input 
            font-size 28px
            flex 1
            background #ffffff
            border-radius 5px
            margin-top 12px
            margin-left 20px
            height 64px
            color #cccccc
            line-height 64px
            padding-left 20px
        
</style>

