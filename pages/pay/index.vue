<template>
  <div class="pay">
    <div class="content">
      <div class="item">
        <div class="item-header">
          <span class="title">车牌号</span>
          <div>
            <span class="num">粤A 2345679</span>
            <span class="type">新能源</span>
          </div>
        </div>
        <div class="item-content">
          <div>
            <span>停车费用</span>
            <span>支付状态</span>
          </div>
          <div>
            <span>
              <span class="money">25.00</span>
              <span class="mini">元</span>
            </span>
            <span class="bold">待支付</span>
          </div>
        </div>
      </div>
      <div class="item">
        <div class="item-content">
          <div>
            <span>支付编码</span>
            <span>12346634674</span>
          </div>
          <div>
            <span>应收金额</span>
            <span>
              <span class="bold">30.00</span>
              <span>元</span>
            </span>
          </div>
          <div>
            <span>优惠金额</span>
            <span>
              <span class="bold">-5.00</span>
              <span>元</span>
            </span>
          </div>
        </div>
      </div>
    </div>
    <div class="btn">确定支付</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      
    }
  }
}
</script>

<style lang="scss" scoped>
.pay{
  font-size: 28rpx;
  color: #333333;
  .content{
    .item{
      box-shadow: 0px 0px 20rpx 0px rgba(41, 167, 139, 0.16);
      border-radius: 20rpx;
      // margin-bottom: 30rpx;
      margin: 0 30rpx 30rpx;
      padding: 30rpx;
      .item-header{
        border-bottom: 2rpx dashed #E4E4E4;
        &>div{
          // margin-top: 15rpx;
          padding: 15rpx 0;
          display: flex;
          align-items: center;
        }
        .num{
          font-size: 36rpx;
          font-weight: bold;
        }
        .type{
          display: inline-block;
          text-align: center;
          width: 100rpx;
          height: 36rpx;
          line-height: 36rpx;
          background: #009D7A;
          border-radius: 6rpx;
          font-size: 24rpx;
          color: #FFFFFF;
          margin-left: 20rpx;
        }
      }
      .item-content{
        &>div{
          margin-top: 16rpx;
          display: flex;
          align-items: center;
          &>span:first-child{
            flex: 1;
          }
          .money{
            font-size: 40rpx;
            font-weight: 800;
            color: #FF8B36;
          }
          .mini{
            font-size: 24rpx;
          }
          .bold{
            font-weight: 800;
          }
        }
      }
    }
  }
  .btn{
    height: 80rpx;
    line-height: 80rpx;
    width: 472rpx;
    text-align: center;
    background: linear-gradient(0deg, #009D7A 0%, #00C89C 100%);
    box-shadow: 0px 14rpx 21rpx 0rpx rgba(10, 160, 127, 0.28);
    border-radius: 40rpx;
    font-size: 28rpx;
    font-weight: bold;
    color: #FFFFFF;
    // margin: 120rpx auto 0;
    position: fixed;
    bottom: 60rpx;
    left: 50%;
    transform: translateX(-50%);
    &.dis{
      background: linear-gradient(0deg, #009D7A 0%, #00C89C 100%);
      box-shadow: 0rpx 14rpx 21rpx 0rpx rgba(10, 160, 127, 0.28);
      opacity: 0.5;
    }
  }
}
</style>