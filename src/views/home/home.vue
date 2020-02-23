<template>
  <div id="home">
        <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <tab-control class="tabcontrol2 tabcontrol"
                 :titles="['流行','新款','精选']"
                 @tabClick="tabClick"
                 ref="tabcontrol1"

                 v-show="isTabFixed"
    ></tab-control>
        <scroll class="content"
                ref="scroll"
                :probetype="3"
                @scroll="contentscroll"
                :pull-up-load="true"
                @pullingup="loadmore">
            <home-swiper :banners="banners" @swiperimgload="swiperimgload"></home-swiper>
            <recommend-view :recommends="recommends"></recommend-view>
            <feature></feature>
            <tab-control class="tabcontrol"
                         :titles="['流行','新款','精选']"
                         @tabClick="tabClick"
                          ref="tabcontrol2"
                         ></tab-control>
            <goods-list :goods="goods[currentType].list" ></goods-list>
        </scroll>
        <back-top @click.native="backtop" v-show="isshow"></back-top>
  </div>
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar'
  import {gethomemultidata,getHomeGoods} from 'network/home'
  import HomeSwiper from './childrencomps/homeswiper'
  import  RecommendView from './childrencomps/RecommendView'
  import Feature from './childrencomps/FeatureView'
  import TabControl from 'components/content/Tabcontrol/TabControl'
  import GoodsList from 'components/content/goods/GoodsList'
  import Scroll from 'components/common/scroll/Scroll'
  import BackTop from 'components/common/backtop/BackTop'
  import {debounce} from "../../components/utils/utils"



    export default {
        name: "home",
        components:{
          NavBar,
          HomeSwiper,
          RecommendView,
          Feature,
          TabControl,
          GoodsList,
          Scroll,
          BackTop,

        },
      data(){
        return {
          banners: [],
          recommends:[],
          goods: {
            'pop':{page : 0, list: []},
            'new':{page : 0, list: []},
            'sell':{page : 0, list: []}
          },
          currentType:'pop',
          isshow : false,
          tabOffsetTop:0,
          isTabFixed:false,
          saveY : -1000
        }
      },
      created() {
          this.gethomemultidata()
          this.getHomeGoods('pop')
          this.getHomeGoods('new')
          this.getHomeGoods('sell')

      },
      mounted(){
        const refresh = debounce(this.$refs.scroll.refresh,)
        this.$bus.$on('itemimgLoad',()=>{
          refresh()
        })

      },
      methods:{
          gethomemultidata(){
            gethomemultidata().then(res =>{
              this.banners = res.data.data.banner.list;
              this.recommends = res.data.data.recommend.list

            })
          },
          getHomeGoods(type){
            const page = this.goods[type].page + 1
          getHomeGoods(type,page).then(res=>{
            this.goods[type].list.push(...res.data.data.list);
            this.goods[type].page += 1
            this.$refs.scroll. finishPullUp()


          })
        },
          tabClick(index){
            switch (index) {
              case 0:
                this.currentType = 'pop'
                break
              case 1:
                this.currentType = 'new'
                break
              case 2 :
                this.currentType = 'sell'
                    break

            }
            this.$refs.tabcontrol2.currentIndex = index
            this.$refs.tabcontrol1.currentIndex = index


          },
          backtop(){
          this.$refs.scroll.scrollTo(0,0,500)
        },
          contentscroll(position){
            this.isshow = -position.y > 1000
            this.isTabFixed = -position.y > this.tabOffsetTop
          },
        loadmore(){
            this.getHomeGoods(this.currentType)
        },
        swiperimgload(){
        this.tabOffsetTop = this.$refs.tabcontrol2.$el.offsetTop
        }
          },
        activated() {
          this.$refs.scroll.scroll.scrollTo(0,this.saveY,0)
          this.$refs.scroll.refresh()
        },
        deactivated() {
          this.saveY = this.$refs.scroll.getScrollY()

        }


    }
</script>

<style scoped>
  #home{

    height: 100vh;
    position: relative;
  }

  .home-nav{
    background-color: var(--color-tint);
    color:white;
    font-size: 22px;

    /*position: fixed;*/
    /*left: 0;*/
    /*right: 0;*/
    /*top: 0;*/
    /*z-index: 9;*/
  }

  .content{
    position: absolute;
    top: 44px;
    bottom: 49px;
    overflow: hidden;
  }
.tabcontrol2{
  position: relative;
  z-index: 9;
}


</style>
