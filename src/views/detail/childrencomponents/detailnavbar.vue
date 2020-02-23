<template>
  <nav-bar>
    <div slot="left" class="backbtn" @click="backclick"><img src="~assets/img/common/back.svg" alt=""></div>
    <div slot="center" class="titles">
    <div v-for="(item,index) in titles" class="title-item" @click="navclick(index)"
    :class="{active : index === currentIndex}">{{item}}</div>
  </div>
  </nav-bar>
    
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar'
    export default {
        name: "detailnavbar",
      components: {
          NavBar
        },
      data(){
          return{
            titles: ['商品','参数','评论','推荐'],
            currentIndex : 0
          }
      },
      methods:{
          navclick(index){
            this.currentIndex = index
          },
          backclick(){
            this.$router.back()
          }
      }

    }
</script>

<style scoped>
  .titles{
    display: flex;
  }
  .title-item{
    flex: 1;
    margin-top: 2px;
  }
  .active{
    color: deeppink;
  }
  .backbtn img{
    margin-top: 11px;
  }


</style>
