<template>
  <div class="shop-info-widget">
    <div class="info-widget-top" @click="goShop">
      <div class="info-widget-shop-pic">
        <img :src="shopInfo.shopImage" width="65" height="65">
      </div>
      <div class="info-widget-shop-info">
        <span class="info-widget-shop-name">{{shopInfo.shopName}}</span>
        <div class="widget-shop-info-content">
          <div class="info-content-line1">
            <span class="star">
              <v-star :size="24" :score="shopInfo.star"></v-star>
              <span class="star-score">{{shopInfo.star}}</span>
            </span>
            <span class="sell-count">月售{{shopInfo.sellCount}}份</span>
            <span class="delivery-time">{{shopInfo.deliveryTime}}<span class="text">分钟</span></span>
          </div>
          <div class="info-content-line2">
            <span class="min-price">￥{{shopInfo.minPrice}}元起送</span>/<span class="delivery-price">配送费￥{{shopInfo.deliveryPrice}}</span>/<span class="rating-score">评价{{shopInfo.ratingScore}}分</span>
            <span class="distance">{{shopInfo.distance}}km</span>
          </div>
        </div>
      </div>
    </div>
    <div class="info-content-activity">
      <span class="support-icon" :class="classMap[shopInfo.supports[0].type]"></span>
      <span class="support-content">{{shopInfo.supports[0].description}}</span>
      <span class="activity" @click="showActivity" >{{shopInfo.activityCount}}个活动<span class="activity-icon" :class="upButton()"></span></span>
      <ul class="activity-wrap" v-show="activityShow">
        <li class="activity-item" v-for="(item, index) in shopInfo.supports" v-if="index!==0" >
          <span class="activity-icon" :class="classMap[item.type]"></span>
          <span class="activity-desc">{{item.description}}</span>
        </li>
      </ul>
    </div>
    <div class="shop-info-widget-splits"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  import Star from '../../components/star/star.vue';
  export default{
    props: {
      shopInfo: {
        type: Object
      }
    },
    created() {
      this.classMap = ['new', 'special', 'decrease'];
      this.upMap = ['up-on', 'up-off'];
    },
    data() {
      return {
        activityShow: true
      };
    },
    methods: {
      goGood() {
        this.$router.push({path: '/shops/goods', query: { shopId: 1, goodId: 0 }});
      },
      goShop() {
        this.$router.push({path: '/shops', query: {shopId: 1}});
      },
      showActivity() {
        this.activityShow = !this.activityShow;
        this.$emit('refresh');
      },
      upButton() {
        if (this.activityShow) {
          return 'up-on';
        } else {
          return 'up-off';
        }
      }
    },
    components: {
      'v-star': Star
    }
  };
</script>

<style lang="stylus" type="text/stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"
  .shop-info-widget
    width 100%
    display block
    .shop-info-widget-splits
      width 100%
      height 5px
      background #f3f3f3
    .info-widget-top
      height 65px
      padding-top 15px
      padding-left 10px
      padding-right 15px
      display flex
      .info-widget-shop-pic
        display block
        width 65px
        height 65px
        flex 0 0 65px
      .info-widget-shop-info
        display inline-block
        flex 1
        padding-left 15px
        .info-widget-shop-name
          display inline-block
          padding-top 4px
          font-family "PingFang SC"
          font-size 16px
          color #37373b
          font-weight 700
        .widget-shop-info-content
          font-family "PingFang SC"
          font-size 11px
          .info-content-line1
            position relative
            color #707072
            padding-top 10px
            display block
            .star
              display inline-block
              .star-score
                padding-left 10px
                font-size 11px
            .sell-count
              font-size 11px
              padding-left 5px
              border-left 1px solid #cfd0cb
            .delivery-time
              right 0
              color #ff5339
              position absolute
              font-size 10px
              .text
                font-size 9px
          .info-content-line2
            position relative
            color #707072
            padding-top 10px
            .distance
              padding-top 3px
              position absolute
              right 0
              font-size 9px
              color #c9c9c9
    .info-content-activity
      font-family "PingFang SC"
      font-size 11px
      position relative
      color #aeaeaf
      padding-top 10px
      display block
      padding-bottom 7px
      padding-left 90px
      .support-icon
        display inline-block
        vertical-align top
        width 13px
        height 13px
        background-size 13px 13px
        background-repeat no-repeat
        &.new
          bg-image(new_3)
        &.special
          bg-image(special_3)
        &.decrease
          bg-image(decrease_3)
      .support-content
        display inline-block
        vertical-align top
        padding-bottom 7px
        @media only screen and (max-width: 320px)
          font-size 10px
          width 130px
          text-overflow ellipsis
          overflow hidden
          white-space: nowrap
      .activity
        display inline-block
        position absolute
        right 15px
        font-size 9px
        color #c9c9c9
        .activity-icon
          display inline-block
          margin-left 5px
          width 11px
          height 6px
          background-size 11px 6px
          background-repeat no-repeat
          &.up-on
            bg-image(up_on)
          &.up-off
            bg-image(up_off)
      .activity-wrap
        margin-right 15px
        position relative
        .activity-item
          padding-bottom 7px
          display block
          .activity-icon
            display inline-block
            vertical-align top
            width 13px
            height 13px
            background-size 13px 13px
            background-repeat no-repeat
            &.new
              bg-image(new_3)
            &.special
              bg-image(special_3)
            &.decrease
              bg-image(decrease_3)
          .activity-desc
            display inline-block
            vertical-align top
            font-family "PingFang SC"
            font-size 11px
            color #aeaeaf
</style>
