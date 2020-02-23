<template>
    <div id="detail">
      <detail-navbar></detail-navbar>
      <detail-swiper :top-images="topImg"></detail-swiper>
      <detail-base-info :goods="goods"></detail-base-info>

    </div>
</template>

<script>
  import DetailNavbar from './childrencomponents/detailnavbar'
  import  {getdetaildata,Goods} from 'network/detail'
  import DetailSwiper from './childrencomponents/detailswiper'
  import DetailBaseInfo from './childrencomponents/DetailBaseInfo'
    export default {
        name: "detail",
      data(){
          return{
            iid : null,
            topImg:[],
            goods: {}
          }
      },
      components:{
        DetailNavbar,
        DetailSwiper,
        DetailBaseInfo
      },
      created() {
          this.iid = this.$route.params.iid
          getdetaildata(this.iid).then(res => {
            const  data = res.data.result;
            this.topImg = res.data.result.itemInfo.topImages
            this.goods= new Goods(data.itemInfo,data.columns,data.shopInfo.services)
          })
      }

    }
</script>

<style scoped>

</style>
