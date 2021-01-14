<template>
	<view class="goods_list">
		<view class="goods_item" @click="navigat(item.id)" 
			v-for="item in goods" :key="item.id">
			<!-- 图片链接失效，请更新数据库 -->
			<image src="../../static/404.png"></image>
			<view class="price">
				<text>￥{{item.sell_price}}</text>
				<text>￥{{item.market_price}}</text>
			</view>
			<view class="name">
				{{item.title}}
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				
			}
		},
		props:['goods'],
		methods:{
			navigat(id){
				this.$emit('goodsItemClick',id)
			}
		}
	}
</script>

<style lang="scss">
	.goods_list{
		padding: 0 15px;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		font-size: 24rpx;
		.goods_item{
			background-color: #fff;
			width: 335rpx;
			margin: 10rpx 0;
			padding: 15rpx;
			box-sizing: border-box;
			image{
				display: block;
				margin: auto;
				width: 90%;
				height: 200px;
			}
			.price{
				margin: 10rpx 0;
				color: $shop-color;
				font-size: 36rpx;
				text:nth-child(2){
					color: #ccc;
					font-size: 28rpx;
					margin-left: 17rpx;
					text-decoration: line-through;
				}
			}
			.name{
				font-size: 28rpx;
				line-height: 40rpx;
			}
		}
	}
</style>
