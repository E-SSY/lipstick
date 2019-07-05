<template>
    <div>
        <div class="search">
            <input v-model="keyword" class="search-input" type="text" placeholder="输入城市名或拼音">
            <div 
                class="search-content" 
                ref="wrapper"
                v-show="keyword"
            >
                <ul>
                    <li class="search-item border-bottom" 
                        v-for="item of list" 
                        :key="item.id"
                        @click="handleCityClick(item.name)"
                    >{{item.name}}</li>
                    <li class="search-item border-bottom" v-show="hasNoData">没有找到匹配数据</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
import Bscroll from 'better-scroll'
export default {
    name:'CitySearch',
    props:{
        cities:Object
    },
    data(){
        return{
            keyword:'',
            list:[],
            timer:null
        }
    },
    methods:{
        handleCityClick(city){
            this.$store.dispatch('changeCity',city)
            this.$router.push('/')
            console.log(this.$store.state.city)
        }
    },

    watch:{
        keyword(){
            if(this.timer){
                clearTimeout(this.timer)
            }
            if(!this.keyword){
                this.list=[]
                return
            }
            this.timer = setTimeout(() => {
                const result = []
                for(let i in this.cities){
                    this.cities[i].forEach((value) => {
                        if(value.spell.indexOf(this.keyword)>-1||value.name.indexOf(this.keyword)>-1){
                            result.push(value)
                        }
                    });
                }
                this.list=result
            }, 100);
        }
    },
    computed:{
        hasNoData(){
            return !this.list.length
        }
    },
    mounted(){
        this.scroll = new Bscroll(this.$refs.wrapper)//引用better-scroll
    },
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl';
.search
    height 72px
    background $bgColor
    padding 10px
    .search-input 
        width 98%
        height 62px
        padding 0 10px
        color #666
        border-radius 6px
        text-align center
        background #ffffff
.search-content
    position absolute
    overflow hidden
    top 170px
    left 0
    right 0
    bottom 0
    background #eee 
    z-index 3
    .search-item
        line-height 65px
        background #ffffff
        color #666
        font-size 28px
        padding-left 10px
</style>
