<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar"/>
      </div>
      <div class="content">
        <div class="title">
            <span class="brand"></span>
            <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
            {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[1].type]"></span>
          <span class="text">{{seller.supports[1].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count" @click="showDetail">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span><span class="bulletin-text"> {{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%"/>
    </div>

    <transition name="fade">
       <div v-show="detailShow" class="detail">
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
              <h1 class="detail-name">{{seller.name}}</h1>
              <div class="star-wrapper">
                <star :size="48" :score="seller.score"></star>
              </div>
              <div class="line-title">
                  <!--line使用span在某些Android浏览器中会出现兼容性问题-->
                <div class="line"></div>
                <div class="text">优惠信息</div>
                <div class="line"></div>
              </div>
              <ul v-if="seller.supports" class="supports">
                <li class="supports-item" v-for="(item ,index) in seller.supports">
                  <span class="icon" :class="classMap[seller.supports[index].type]"></span>
                  <span class="text">{{seller.supports[index].description}}</span>
                </li>
              </ul> 
              <div class="line-title">
                  <!--line使用span在某些Android浏览器中会出现兼容性问题-->
                <div class="line"></div>
                <div class="text">商家公告</div>
                <div class="line"></div>
              </div>  
              <div class="bulletin">
                <p class="content">{{seller.bulletin}}</p>
              </div>         
            </div>
        </div>
          <div class="detail-close" @click="hiddenDetail">
            <i class="icon-close"></i>
          </div>
      </div>
    </transition>  
  
  </div>
</template>
<script type="text/ecmascript-6">
  import star from '../star/star';
  export default{
    props: {
      seller: {
        type: Object
      }
    },
    data () {
      return {
        detailShow: false
      };
    },
    methods: {
      showDetail () {
        this.detailShow = true;
      },
      hiddenDetail () {
        this.detailShow = false;
      }
    },
    created () {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },
    components: {
      star: star
    }
  };
</script>

<style>
  .header{
    color: #fff;
    position: relative;
    overflow: hidden;
    background: rgba(7, 17, 27, 0.5);
  }
  .content-wrapper{
    position: relative;
    padding:24px 12px 18px 24px;
    font-size: 0;
  }
  .avatar{
    display: inline-block;
    vertical-align: top;
  }
  .avatar> img{
    border-radius: 2px;
  }
  .content{
    display: inline-block;
    font-size: 14px;
    margin-left: 16px;
  }
  .content>.title{
    margin: 2px 0 8px 0;
  }
  .title>.brand{
    vertical-align: top;
    display: inline-block;
    width: 30px;
    height: 18px;
    background:url('brand@2x.png') no-repeat;
    background-size: 30px 18px;
    @media (-webkit-min-device-pixel-ratio: 3), (min-device-pixel-ratio: 3){
        backgorund:url('brand@3x.png') no-repeat;
    }
  }
  .content> .title>.name{
    margin-left: 6px;
    font-size: 16px;
    line-height: 16px;
    color: rgb(255, 255, 255);
    font-weight: bold;
  }
  .content> .description{
    margin-bottom: 10px;
    line-height:12px;
    font-size: 12px;
  }
  .content> .support >.icon{
    display: inline-block;
    vertical-align: top;
    width: 12px;
    height: 12px;
    margin-right: 4px;
    background-size: 12px 12px;
    background-repeat: no-repeat;
  }
  .support >.decrease{
    background:url("decrease_1@2x.png");
    @media (-webkit-min-device-pixel-ratio: 3), (min-device-pixel-ratio: 3){
       backgorund:url('decrease_1@3x.png');
    }
  }
    .support >.discount{
    background:url("discount_1@2x.png");
    @media (-webkit-min-device-pixel-ratio: 3), (min-device-pixel-ratio: 3){
       backgorund:url('discount_1@3x.png');
    }
  }
   .support >.invoice{
    background:url("invoice_1@2x.png");
    @media (-webkit-min-device-pixel-ratio: 3), (min-device-pixel-ratio: 3){
       backgorund:url('invoice_1@3x.png');
    }
  }
    .support >.guarantee{
    background:url("guarantee_1@2x.png");
    @media (-webkit-min-device-pixel-ratio: 3), (min-device-pixel-ratio: 3){
       backgorund:url('guarantee_1@3x.png');
    }
  }
    .support >.special{
    background:url("special_1@2x.png");
    @media (-webkit-min-device-pixel-ratio: 3), (min-device-pixel-ratio: 3){
       backgorund:url('special_1@3x.png');
    }
  }
  .support>.text{
    line-height: 12px;
    font-size: 10px;
  }
  @import '../../common/stylus/style.css';

  .support-count{
    position: absolute;
    right: 12px;
    bottom: 14px;
    padding:0 8px;
    height: 24px;
    line-height: 24px;
    border-radius: 14px;
    background: rgba(0, 0, 0, 0.2);
    text-align: center;
  }
  .support-count>.count + .icon-keyboard_arrow_right{
    font-size: 10px;
    line-height: 24px;
    margin-left: 2px;
  }
  .bulletin-wrapper{
    height: 28px;
    line-height: 28px;
    padding:0 22px 0 12px;
    position: relative;
    /*实现...*/
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis; 
    /*font-size: 0;消除span之间由于空格产生的间隙*/
    background: rgba(7, 17, 27, 0.2);
  }
  .bulletin-title{
    display: inline-block;
    width: 22px;
    height: 12px;
    margin-top: 8px;
    vertical-align: top;
    background:url('bulletin@2x.png') no-repeat;
    background-size: 22px 12px;
    @media (-webkit-min-device-pixel-ratio: 3) ,(min-device-pixel-ratio: 3) {
     background: url('bulletin@3x.png') no-repeat; 
    }
  }
   .bulletin-text{
     margin: 0 4px;
     font-size: 10px;
     font-weight: 200;
     vertical-align: top;
  }
  .bulletin-wrapper>.icon-keyboard_arrow_right{
    position: absolute;
    top: 9px;
    right: 12px;
    font-size: 10px;
  }
  .background{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
    filter: blur(10px);
  }
  /*弹出层style*/
  .detail{
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 100;
    overflow: auto;
    /*transition: all 0.5s;*/
    -webkit-backdrop-filter: blur(10px);
    opacity: 1;
    background: rgba(7, 17, 27, 0.8);
  }
  /*vue2.0 升级*/
   .fade-enter-active, .fade-leave-active{
    transition: all 0.5s;
  }
  .fade-enter,.fade-leave-to{
    opacity: 0;
    background: rgba(7, 17, 27, 0);
  }
 /*.fade-enter,.fade-leave{
    opacity: 1;
    background: rgba(7, 17, 27, 0);
  } */
  /*清除浮动*/
  .clearfix{
    display: inline-block;
  }
  .clearfix:after{
    display: block;
    content: ".";
    height: 0;
    line-height: 0;
    clear: both;
    visibility: hidden;
  }
  .detail-wrapper{
    min-height: 100%;
    width: 100%;
  }
  .detail-main{
    margin-top: 64px;
    padding-bottom: 64px;
  }
  .detail-name{
    line-height: 16px;
    text-align: center;
    font-size: 16px;
    font-weight: 700;
  }
  .star-wrapper{
    margin-top: 18px;
    padding: 2px 0;
    text-align: center;
  }
 .line-title{
    /*布局的代码放到前面*/
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    /*自身的样式放到后面*/
    width: 80%;
    margin: 28px auto 24px auto;
  }
  .line-title>.line{
    -webkit-box-flex: 1;
    -ms-flex: 1;
    flex: 1;
    position: relative;
    top: -6px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  }
  .line-title> .text{
    padding: 0 12px;
    font-size: 14px;
    font-weight: 700;
  }
  .supports{
    width: 100%;
    margin: 0 auto;
  }
  .bulletin{
    width: 80%;
    margin: 0 auto;
  }
  .bulletin> .content{
    padding: 0 12px;
    line-height: 24px;
    font-size: 12px;
  }
  .supports-item{
    padding: 0 40px;
    margin-bottom: 12px;
    font-size: 0;
  }
  .supports-item:last-child{
    margin-bottom: 0;
  }
  .supports-item> .icon{
    display: inline-block;
    width: 32px;
    height: 32px;
    vertical-align: top;
    margin-right: 6px;
    background-size: 16px 16px;
    background-repeat: no-repeat;
  }
    .supports-item >.decrease{
      background:url("decrease_2@2x.png");
      @media (-webkit-min-device-pixel-ratio: 3), (min-device-pixel-ratio: 3){
        backgorund:url('decrease_2@3x.png');
      }
    }
    .supports-item >.discount{
      background:url("discount_2@2x.png");
      @media (-webkit-min-device-pixel-ratio: 3), (min-device-pixel-ratio: 3){
        backgorund:url('discount_2@3x.png');
      }
    }
   .supports-item >.invoice{
      background:url("invoice_2@2x.png");
      @media (-webkit-min-device-pixel-ratio: 3), (min-device-pixel-ratio: 3){
        backgorund:url('invoice_2@3x.png');
      }
    }
    .supports-item >.guarantee{
      background:url("guarantee_2@2x.png");
      @media (-webkit-min-device-pixel-ratio: 3), (min-device-pixel-ratio: 3){
        backgorund:url('guarantee_2@3x.png');
      }
    }
  .supports-item >.special{
    background:url("special_2@2x.png");
    @media (-webkit-min-device-pixel-ratio: 3), (min-device-pixel-ratio: 3){
       backgorund:url('special_2@3x.png');
    }
  }
  .supports-item> .text{
    line-height: 16px;
    font-size: 12px;
  }
  .detail-close{
    position: relative;
    width: 32px;
    height: 32px;
    margin: -64px auto 0 auto;
    clear: both;
    font-size: 32px;
  }

</style>
