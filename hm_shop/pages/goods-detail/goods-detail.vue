<template>
	<view class="goods_detail">
		<swiper indicator-dots style="background-color: #FFECEC;">
			<swiper-item v-for="(item,index) in swipers" :key="index">
				<image :src="item.get_src"></image>
			</swiper-item>
		</swiper>
		<!-- 商品价格和标题 -->
		<view class="box1">
			<view class="price">
				<text>￥6788</text>
				<text>￥8788</text>
			</view>
			<view class="goods_name">
				手机名啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊
			</view>
		</view>
		<view class="line"></view>
		<!-- 货号库存 -->
		<view class="box2">
			<view>货号：</view>
			<view>库存：</view>
		</view>
		<view class="line"></view>
		<!-- 详情介绍内容 -->
		<view class="box3">
			<view class="tit">
				详情介绍
			</view>
			<view class="content">
				内容
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id:0,
				swipers:[]
			}
		},
		methods: {
			// 获取商品轮播图数据
			async getSwipers(){
				const res = await this.$myRuquest({
					url:'/api/getthumimages/'+this.id
				})
				this.swipers = res.data.message
				console.log(this.swipers)
			}
		},
		onLoad(options) {
			this.id = options.id
			this.getSwipers()
		}
	}
</script>

<style lang="scss">
.line{
	width: 750rpx;
	height: 10rpx;
	background-color: #eee;
}
.goods_detail{
	swiper{
		width: 750rpx;
		image{
			width: 100%;
			height: 100%;
		}
	}
	.box1{
		padding: 10px;
		.price{
			font-size: 35rpx;
			color: $shop-color;
			line-height: 80rpx;
			text:nth-child(2){
				color: #ccc;
				font-size: 28rpx;
				text-decoration: line-through;
				margin-left: 20rpx;
			}
		}
		.goods_name{
			font-size: 32rpx;
			line-height: 60rpx;
		}
	}
	.box2{
		padding: 0 10px;
		font-size: 32rpx;
		line-height: 66rpx;
	}
	.box3{
		.tit{
			padding: 0 10rpx;
			font-size: 32rpx;
			border-bottom:1px solid #eee ;
			line-height: 70rpx;
		}
		.content{
			padding: 10px;
			font-size: 28rpx;
			color: #333;
		}
	}
}
</style>
