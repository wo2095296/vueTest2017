<template>
<div class="header">
  <div class="content-warpper">
  <div v-if="seller.supports" class="support-count" @click="showDetail">
      <span class="count">{{seller.supports.length}}个</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>  
    <div class="avatar">
      <img :src="seller.avatar" width="64" height="64" alt="">
    </div>
    <div class="content">
  
      <div class="title">
        <span class="brand"></span>
        <span class="name">{{seller.name}}</span>
      </div>
      <div class="description">
        {{seller.description}}/{{seller.deliveryTime}}分钟送达
      </div>
      <div v-if="seller.supports" class="support" @click="showDetail">
        <span class="icon" :class="classMap[seller.supports[0].type]"></span>
        <span class="text">{{seller.supports[0].description}}</span>
      </div>
    </div>
  </div>
  <div class="bulletin-warpper">
    <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span><i class="icon-keyboard_arrow_right"></i>
  </div>
  <div class="background" >
    <img :src="seller.avatar" width="100%" height="100%" >
  </div>
  <div class="detail" v-show="detailShow" transition="fade">
    <div class="detail-wrapper clearfix">
      <div class="detail-main">
        <h1 class="name">{{seller.name}}</h1>
          <div class="star-wrapper">
            <v-star :size="48" :score="seller.score"></v-star>
          </div>
          <div class="title">
            <div class="line"></div>
            <div class="text">优惠信息</div>
            <div class="line"></div>
          </div>
          <ul v-if="seller.supports" class="supports">
            <li class="support-item" v-for="(item,index) in seller.supports">
              <span class="icon" :class="classMap[seller.supports[index].type]"></span>
              <span class="text">{{seller.supports[index].description}}</span>
            </li>
          </ul>
          <div class="title">
            <div class="line"></div>
            <div class="text">商家公告</div>
            <div class="line"></div>
          </div>     
          <div class="bulletin">
            <p class="content" v-text="seller.bulletin">
              
            </p>
          </div>     
      </div>
    </div>
    <div class="detail-close" @click="hideDetail">
      <i class="icon-close"></i>
    </div>
  </div>
</div>
 
</template>

<script>
import star from '@/components/star/star'
export default {
  name: 'header',
  props:{
    seller:{
      type:Object
    }
  },
  data() {
    return {
      detailShow:false
    }
  },
  methods:{
    showDetail() {
      this.detailShow=true;
    },
    hideDetail() {
      this.detailShow=false;
    }      
    
  },
  components:{
    'v-star':star
  },
  created(){
    this.classMap=['decrease','discount','special','invoice','guarantee'];
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import "../../common/stylus/mixin.styl";
@import "../../common/stylus/header.styl";
</style>
