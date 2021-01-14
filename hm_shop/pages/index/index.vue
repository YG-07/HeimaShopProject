<template>
	<view class="home">
		<swiper indicator-dots circular autoplay interval="3000" duration="200">
			<swiper-item v-for="item in swipers" :key="item.id">
				<a :href="item.url">
					<image :src="item.img"></image>
				</a>
			</swiper-item>
		</swiper>
		<!-- 导航区域 -->
		<view class="nav">
			<view class="nav-item" v-for="(item,index) in navs" :key="index" @click="navItemClick(item.path)">
				<view class="img" :class="item.icon"></view>
				<view class="txt">{{item.title}}</view>
			</view>
		</view>
		<!-- 推荐商品 -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<goods-list :goods="goods"></goods-list>
		</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	
	export default {
		components:{
			goodsList
		},
		data() {
			return {
				swipers:[],
				goods:[],
				navs:[
					{
						icon:'iconfont icon-mall',
						title:'黑马超市',
						path:'/pages/goods/goods'
					},
					{
						icon:'iconfont icon-telephone',
						title:'联系我们',
						path:'/pages/contact/contact'
					},
					{
						icon:'iconfont icon-picture',
						title:'社区图片',
						path:'/pages/pics/pics'
					},
					{
						icon:'iconfont icon-comment',
						title:'学习资料',
						path:'/pages'
					},
				]
			}
		},
		onLoad() {
			this.getSwipers()
			this.getHotGoods()
		},
		methods: {
			// 获取轮播图数据
			async getSwipers(){
				const res=await this.$myRuquest({
					url:'/api/getlunbo'
				})
				this.swipers=res.data.message
				// console.log(this.swipers)
			},
			// 获取热门商品数据
			async getHotGoods(){
				const res=await this.$myRuquest({
					url:'/api/getgoods?pageindex=1'
				})
				this.goods=res.data.message
			},
			navItemClick(url){
				uni.navigateTo({
					url
				})
			}
		}
	}
</script>

<style lang="scss">
	.home{
		swiper{
			width: 750rpx;
			height: 380rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
		.hot_goods{
			background-color: #eee;
			overflow: hidden;
			.tit{
				margin: 7px 0;
				background-color: #fff;
				color: $shop-color;
				height: 50px;
				line-height: 50px;
				text-align: center;
				letter-spacing: 20px;
			}
			
		}
	}
	.nav{
		display: flex;
		width: 750rpx;
		text-align: center;
	}
	.nav-item{
		flex:1;
		text-align: center;
	}
	.img{
		margin: 20rpx auto;
		width: 120rpx;
		height: 120rpx;
		line-height: 120rpx;
		background: #F67B66;
		border-radius: 50%;
	}
	.txt{
		margin-bottom: 20rpx;
		font-size: 30rpx;
	}
	.iconfont {
		color: #fff;
		font-size: 50rpx;
	}
</style>
