<template>
  <div class="header">
    <div class="content-wrap">
      <div class="avatar">
        <img :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <div class="title">
          <div class="brand"></div>
          <div class="name">{{seller.name}}</div>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" @click="showDetail">
          <div class="supports-type" :class="classMap[seller.supports[0].type]"></div>
          <div class="supports-description">{{seller.supports[0].description}}</div>
        </div>
      </div>
      <div class="support-count" v-if="seller.supports" @click="showDetail">
        {{seller.supports.length}}个
        <i class="icon-keyboard_arrow_right "></i> 
      </div>
    </div>
    <div class="bulletin-wrap" @click="showDetail">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="bgd">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <transition name="fade">
      <div v-show="detailshow" class="detail">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
          <h1 class="name">{{seller.name}}</h1>
          <div class="starWapper">
            <star :size="48" :score="seller.score"></star>
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
            <p class="content">
              {{seller.bulletin}}
            </p>
          </div>
        </div>
      </div>
      <div class="detail-close" @click="hideDetail">
        <i class="icon-close"></i>
      </div>
    </div>
    </transition>
  </div>
</template>
 
<script>
import star from "../../components/star/star";
export default {
  name: "headTop",
  props: {
    seller: {
      type: Object
    }
  },
  data() {
    return {
      detailshow: false
    };
  },
  created() {
    this.classMap = ["decrease", "discount", "special", "invoice", "guarantee"];
  },
  methods: {
    showDetail() {
      this.detailshow = true;
    },
    hideDetail() {
      this.detailshow = false;
    }
  },
  components: {
    star
  }
};
</script> 

<style lang="stylus">
@import '../../common/stylus/mixin'
.header
  position: relative
  overflow: hidden
  color: #fff
  background: rgba(7, 17, 27, 0.5)
  .content-wrap
    font-size: 0
    position: relative
    .avatar
      display: inline-block
      padding: 24px 16px 18px 24px
      vertical-align: top
      img
        width: 64px
        height: 64px
        border-radius: 4px
    .content
      display: inline-block
      .title
        margin: 26px auto 8px auto
        .brand
          display: inline-block
          bg-image(brand)
          background-size: 30px 18px
          background-repeat: no-repeat
          vertical-align: top
          width: 30px
          height: 18px
        .name
          display: inline-block
          font-size: 16px
          color: #ffffff
          font-weight: bold
          line-height: 18px
          margin-left: 6px
      .description
        margin-bottom: 10px
        line-height: 12px
        font-size: 12px
        margin-bottom: 10px
      .supports-type
        display: inline-block
        vertical-align: top
        width: 12px
        height: 12px
        margin-right: 4px
        background-size: 12px 12px
        background-repeat: no-repeat
        &.decrease
          bg-image(decrease_1)
        &.discount
          bg-image(discount_1)
        &.guarantee
          bg-image(guarantee_1)
        &.invoice
          bg-image(invoice_1)
        &.special
          bg-image(special_1)
      .supports-description
        display: inline-block
        font-size: 10px
        line-height: 12px
    .support-count
      position: absolute
      right: 12px
      bottom: 16px
      padding: 7px 8px
      font-size: 10px
      line-height: 12px
      background-color: rgba(0, 0, 0, 0.2)
      border-radius: 14px
  .bulletin-wrap
    position: relative
    height: 28px
    line-height: 28px
    padding: 0 22px 0 12px
    white-space: nowrap
    overflow: hidden
    text-overflow: ellipsis
    background: rgba(7, 17, 27, 0.2)
    .bulletin-title
      display: inline-block
      vertical-align: top
      margin-top: 8px
      width: 22px
      height: 12px
      bg-image('bulletin')
      background-size: 22px 12px
      background-repeat: no-repeat
    .bulletin-text
      vertical-align: top
      margin: 0 4px
      font-size: 10px
    .icon-keyboard_arrow_right
      position: absolute
      font-size: 10px
      right: 12px
      top: 8px
  .bgd
    position: absolute
    top: 0
    left: 0
    z-index: -1
    width: 100%
    height: 100%
    background-color: rgba(7, 17, 27, 0.5)
    filter: blur(10px)
  .detail
    position: fixed
    z-index: 100
    top: 0
    left: 0
    width: 100%
    height: 100%
    overflow: auto
    opacity: 1 // 这是动画设置
    background: rgba(7, 17, 27, 0.8)
    &.fade-enter-active, &.fade-leave-active // vue的动画需要参考vue动画配置理解
      transition: all 0.5s
    &.fade-enter, &.fade-leave-active
      opacity: 0
      background: rgba(7, 17, 27, 0)
    .detail-wrapper
      min-height: 100%
      width: 100%
      .detail-main
        margin-top: 64px
        padding-bottom: 64px
        .name
          line-height: 16px
          font-size: 16px
          font-weight: 700
          text-align: center
        .starWapper
          margin-top: 18px
          padding: 2px 0
          text-align: center
        .title
          display: flex
          width: 80%
          margin: 28px auto 24px
          .line
            flex: 1
            position: relative
            top: -6px
            border-bottom: 1px solid rgba(255, 255, 255, 0.2)
          .text
            padding: 0 12px
            font-size: 14px
            font-weight: 700
        .supports
          width: 80%
          margin: 0 auto
          .support-item
            padding: 0 12px
            margin-bottom: 12px
            font-size: 0
            &:last-child
              margin-bottom: 0
            .icon
              display: inline-block
              width: 16px
              height: 16px
              vertical-align: top
              margin-right: 6px
              background-size: 12px 12px
              background-repeat: no-repeat
              &.decrease
                bg-image(decrease_2)
              &.discount
                bg-image(discount_2)
              &.guarantee
                bg-image(guarantee_2)
              &.invoice
                bg-image(invoice_2)
              &.special
                bg-image(special_2)
            .text
              font-size: 12px
              line-height: 16px
        .bulletin
          width: 80%
          margin: 0 auto
          .content
            padding: 0 12px
            line-height: 24px
            font-size: 12px
    .detail-close
      position: relative
      width: 32px
      height: 32px
      margin: -64px auto 0 auto
      font-size: 32px
      color: rgba(255, 255, 255, 0.5)
</style>