<template>
	<view class="parkingFee">
		<div class="content">
			<div class="content-top">
				<div class="title">{{type === 1 ? '普通车牌' : '新能源车牌'}}</div>
				<div class="switch" @click="switchType">
					<img src="./../../static/switch.png" alt="">
					<span>{{type !== 1 ? '普通车牌' : '新能源车牌'}}</span>
				</div>
			</div>
			<div class="content-bottom">
				<div v-for="item in type === 1 ? 7 : 8" class="item" :class="{'checked':item == inputValIndex}" :key="'inputVal'+item" @click="showMyInput(true)">{{inputVal[item]}}</div>
			</div>
			<div class="btn" :class="{dis:isDis}" @click="checkFee">查询缴费</div>
		</div>
		<myInput :isShow="inputIsShow" :inputType="inputType" @emitVal="inputValFun" @closeInput="showMyInput"/>
	</view>
</template>

<script>
import myInput from './../../components/myInput/index.vue'
	export default {
		components: {
			myInput
		},
		data() {
			return {
				inputIsShow:false,
				inputVal:[],
				inputValIndex:0, // 当前输入的车牌号位置
				// inputValTypes:'1233334',
				type:1, // 1为普通车牌 2为新能源车牌
				isLoading:false // 是否正在请求中
			}
		},
		onLoad() {

		},
		computed: {
			// 返回车牌对应下标下显示的键盘类型
			inputValTypes(){
				if(this.type == 1) return '1233334'
				else if(this.type == 2) return '12333334'
			},
			// 返回当前需要的键盘类型
			inputType(){
				return this.inputValTypes[this.inputVal.length]
			},
      // 返回是否可以点击确认
      isDis(){
        return (this.type == 1 && this.inputValIndex != 7) || (this.type == 2 && this.inputValIndex != 8) || this.isLoading
      }
		},
		methods: {
			inputValFun(val){
				let index = 0
				if(val == -1 && this.inputVal.length) {
					let i = 1
					if(this.inputVal[0] === '民' && this.inputVal.length <= 2) i = 2
					index -= i
					this.inputVal.splice(this.inputVal.length-i,i)
				} else if(val != -1 && this.inputVal.length !== this.inputValTypes.length) {
					index = 1
					if(val === '民航') {
						this.inputVal.push('民','航')
						index = 2
					} else this.inputVal.push(val)
				}
				this.inputValIndex += index
				if(this.inputVal.length === this.inputValTypes.length) this.inputIsShow = false
			},
			showMyInput(bool){
				this.inputIsShow = bool
			},
			switchType(){
				this.type = this.type == 1 ? 2 : 1
				this.inputVal.splice(0,this.inputVal.length)
				this.inputValIndex = 0
			},
      checkFee(){
        if(this.isDis) return
        uni.navigateTo({
          url: '/pages/pay/index'
        })
      }
		}
	}
</script>

<style lang="scss" scope>
.parkingFee{
	padding: 0 30rpx;
	.content{
		.content-top{
			padding-bottom: 30rpx;
			display: flex;
			.title{
				font-size: 36rpx;
				font-weight: bold;
				color: #333333;
				flex: 1;
			}
			.switch{
				display: flex;
				align-items: center;
				font-size: 28rpx;
				font-weight: 500;
				color: #009D7A;
				img{
					width: 30rpx;
					height: 24rpx;
					margin-right: 17rpx;
				}
			}
		}
		.content-bottom{
			display: flex;
			.item{
				flex: 1;
				height: 100rpx;
				line-height: 100rpx;
				text-align: center;
				border: 2rpx solid #EEEEEE;
				font-size: 36rpx;
				font-weight: 500;
				color: #333333;
				border-right: 0;
				&:nth-child(2){
					margin-right: 20rpx;
				}
				&:nth-child(2), &:last-child{
					border-right: 2rpx solid #EEEEEE;
				}
				&.checked{
					border: 2rpx solid #009D7A;
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
			margin: 120rpx auto 0;
			&.dis{
				background: linear-gradient(0deg, #009D7A 0%, #00C89C 100%);
				box-shadow: 0rpx 14rpx 21rpx 0rpx rgba(10, 160, 127, 0.28);
				opacity: 0.5;
			}
		}
	}
}
	/* .content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	} */
</style>
