<template>
    <div class="shopCart">
        <div class="content">
            <div class="content-left">
                <div class="logo-wrapper">
                    <div class="logo">
                        <i class="icon-shopping_cart"></i>
                    </div>
                </div>
                <div class="price">￥0</div>
                <div class="desc">另需配送费￥{{deliveryPrice}}元</div>
            </div>
            <div class="content-right">
                <div class="pay">
                    ￥{{minPrice}}起送
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  props: {
    deliveryPrice: {
      type: Number,
      default: 0
    },
    minPrice: {
      type: Number,
      default: 0
    }
  }
};
</script>

<style lang="stylus">
.shopCart
    position: fixed
    left: 0
    bottom: 0
    z-index: 50
    width: 100%
    height: 48px
    background: #999
    .content
        display: flex
        background: #141d27
        color: rgba(255, 255, 255, 0.4)
        .content-left
            flex: 1
            font-size: 0
            .logo-wrapper
                display: inline-block
                position: relative
                top: -10px
                margin: 0 12px
                padding: 6px
                width: 56px
                height: 56px
                box-sizing: border-box
                vertical-align: top
                border-radius: 50%
                background: #141d27
                .logo
                    width: 100%
                    height: 100%
                    border-radius: 50%
                    text-align: center
                    background: #2b343c
                    .icon-shopping_cart
                        font-size: 24px
                        line-height: 44px
                        color: #80858a
            .price
                display: inline-block
                vertical-align: top
                line-height: 24px
                margin-top: 12px
                box-sizing: border-box
                padding-right: 12px
                border-right: 1px solid rgba(255, 255, 255, 0.1)
                font-size: 16px
                font-weight: 700
            .desc
                display: inline-block
                vertical-align: top
                margin: 12px 0 0 12px
                line-height: 24px
                font-size: 10px
        .content-right
            flex: 0 0 105px
            width: 105px
            .pay
                height: 48px
                line-height: 48px
                text-align: center
                font-size: 12px
                font-weight: 700
                background: #2b333b
</style>
