<template>
	<view class="constant">
		<image class="img" src="http://www.itcast.cn/2018czydz/images/gywmban.jpg"></image>
		<view class="info">
			<view @click="callMe">联系电话：400-123-4567 (点击拨打)</view>
			<view>校区地址：浙江省杭州市下沙经济开发区4号大街187号盛泰时代山</view>
		</view>
		<map class="map" :longitude="longitude" :latitude="latitude" :scale="scale" :markers="mark"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:120.363172,
				latitude:30.312212,
				scale:13,
				mark:[{
					longitude:120.363172,
					latitude:30.312212,
					iconPath:'../../static/hmlogo.png',
					width:30,
					height:30
				}]
			}
		},
		methods: {
			callMe(){
				uni.makePhoneCall({
					phoneNumber:'400-123-4567'
				})
			}
		}
	}
</script>

<style lang="scss">
	.constant{
		.img{
			width: 750rpx;
			height: 320rpx;
		}
		.info{
			padding: 10rpx 20rpx;
			view{
				padding: 10rpx;
				font-size: 30rpx;
				line-height: 70rpx;
				border: 1px solid #eee ;
			}
		}
	}
	.map{
		width: 750rpx;
		height: 750rpx;
	}
</style>
