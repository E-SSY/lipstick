<template>
    <div>
        <div class="recommend-title">热销推荐</div>
        <ul>
            <li class="item border-bottom" v-for="item of list" :key="item.id">
                <img class="item-img" :src="item.imgUrl">
                <div class="item-info">
                    <p class="item-title">{{item.title}}</p>
                    <p class="item-desc">{{item.desc}}</p>
                    <button class="item-button">查看详情</button>
                </div>
                
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name:'HomeRecommend',
    props:{
        list:Array
    }
}
</script>

<style lang="stylus" scoped>
@import '~styles/mixins.styl';
.recommend-title 
    line-height 70px
    background #eeeeee
    text-indent 20px
    margin-top 10px
.item
    display flex
    height 180px
    overflow hidden
    .item-img
        width 160px
        height 160px
        margin 10px
    .item-info
        flex 1
        min-width 0
        padding 10px
        .item-title
            line-height 44px
            font-size 32px
            ellipsis()
        .item-desc
            line-height 30px
            color #cccccc
            font-size 28px
            margin-top 10px
            ellipsis()
        .item-button
            color #fff
            margin-top 20px
            background #ff9300
            padding 10px 
            border-radius 5px



</style>
