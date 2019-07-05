<template>
    <div class="header">
        <router-link to="/">
            <div class="iconfont header-back">&#xe624;</div>
        </router-link>
        城市选择
    </div>
</template>

<script>
export default {
    name:'CityHeader'
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl';
.header
    overflow hidden
    height $headerHeight
    line-height $headerHeight
    background $bgColor
    color #ffffff
    text-align center
    font-size 32px
    position relative
    .header-back
        position absolute
        top 0
        left 0
        width 64px
        text-align center
        font-size 36px
        color #ffffff
</style>
