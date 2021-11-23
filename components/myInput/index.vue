<template>
	<div class="myInput">
    <template v-if="isShow">
      <div class="header">
        <div class="close" @click="closeInput">关闭</div>
      </div>
      <div class="content">
        <div class="items" v-for="(item,index) in (inputType==1 ? typeArr1:typeArr2)" :key="'key1'+index">
          <div class="item" :class="{'dis':key == 'I' || key == 'O' || (inputType == 2 && key < 10) || (inputType != 4 && key == '字'),'mt2':key.length == 2}" v-for="(key,i) in item" :key="'key2'+i" @click="emitVal" :data-val="key">
            {{key}}
          </div>
        </div>
        <div class="removeKey" @click="removeKey">
          <img src="./../../static/delete.png" alt="">
        </div>
        <div class="items extra" v-if="showExtra">
          <div class="item" v-for="(key,index) in typeArr3" :key="'extra'+index" @click="emitVal" :data-val="key">{{key}}</div>
        </div>
      </div>
    </template>
	</div>
</template>

<script>
	export default{
		props:{
			isShow:{
				type:Boolean,
				default:false
			},
			inputType:{ // 1中文 2英文 3英文数字 4英文数字中文
				type:Number,
				default:1
			}
		},
		data(){
      let typeArr1 =[
        ['京','津','沪','渝','翼','豫','云','辽','黑','湘'],
        ['皖','鲁','新','苏','浙','赣','鄂','桂','甘'],// ,'港'
        ['晋','蒙','陕','吉','闽','贵','粤','青','藏'],// ,'澳'
        ['川','宁','琼','使','WJ','民航'] 
      ]
      let typeArr2 = [
        ['1','2','3','4','5','6','7','8','9','0'],
        ['Q','W','E','R','T','Y','U','I','O','P'],
        ['A','S','D','F','G','H','J','K','L','字'],
        ['Z','X','C','V','B','N','M']
      ]
      let typeArr3 = ['领','警','港','澳','学']
			return {
				typeArr1,
				typeArr2,
        typeArr3,
        showExtra:false
			}
		},
    methods: {
      emitVal(e){
        let val = e.target.dataset.val
        if(this.inputType == 4 && val == '字') this.showExtra = !this.showExtra //弹窗
        else if(!(val == 'I' || val == 'O' || (this.inputType == 2 && val < 10)))this.$emit('emitVal',val)

        if(this.typeArr3.includes(val)) this.showExtra = false
      },
      removeKey(){
        this.$emit('emitVal',-1)
      },
      closeInput(){
        this.showExtra = false
        this.$emit('closeInput',false)
      }
    }
	}
</script>

<style lang="scss">
.myInput {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 10;
  background: #fff;
  // background: darkkhaki;
  border-top: 2rpx solid #EEEEEE;
  .header{
    height: 68rpx;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    .close{
      font-size: 28rpx;
      font-weight: 500;
      color: #009D7A;
      padding-right: 31rpx;
    }
  }
  .content{
    display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
    background: #cfd4db;
    .items{
      display: flex;
      // margin: 5px auto;
      .item{
        padding: 20rpx 10rpx;
        padding: 26rpx 16rpx;
        padding: 26rpx 0;
        padding: 22rpx 0;
        background: #fff;
        border-radius: 10rpx;
        margin: 10rpx 4rpx;
        width: calc(100vw / 10 - 10rpx);
        text-align: center;
        &.dis{
          color: #cfd4db;
        }
        &.mt2{
          padding-left: 12rpx;
          padding-right: 12rpx;
        }
      }
    }
    .extra{
      position: absolute;
      background: rgba(0,0,0,.6);
      padding: 4rpx 8rpx;
      border-radius: 10rpx;
      right: 4rpx;
      bottom: 196rpx;
    }
    .removeKey{
      position: absolute;
      bottom: 10rpx;
      right: 2rpx;
      height: 86rpx;
      border-radius: 10rpx;
      width: 106rpx;
      background: #a8b0bd;
      display: flex;
      justify-content: center;
      align-items: center;
      img{
        width: 67rpx;
        height: 40rpx;
      }
    }
  }
}
</style>
