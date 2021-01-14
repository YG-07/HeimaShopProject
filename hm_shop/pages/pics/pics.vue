<template>
	<view class="pics">
		<scroll-view scroll-y="true" class="left">
			<view v-for="item in cates" 
				:class="currentId===item.id?'active':''"
				@click="leftClickHandle(item.id)" :key="item.id">{{item.title}}</view>
		</scroll-view>
		<scroll-view scroll-y="true" class="right">
			<view class="item" v-for="item in secondData" :key="item.id">
				<!-- 图片链接失效，请更新数据库 -->
				<image src="../../static/404.png"></image>
				<text>{{item.title}}</text>
			</view>
			<view class="isOver">
				-----没有更多了-----
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cates:[],
				currentId:0,
				secondData:[]
			}
		},
		methods: {
			async getPicsCate(){
				const res = await this.$myRuquest({
					url:'/api/getimgcategory'
				})
				this.cates = res.data.message
				this.currentId=this.cates[0].id
				this.leftClickHandle(this.currentId)
			},
			async leftClickHandle(id,callBack){
				this.currentId=id
				// 点击时获取右侧数据
				const res = await this.$myRuquest({
					url:'/api/getimages/'+id
				})
				this.secondData = res.data.message
			}
		},
		onLoad() {
			this.getPicsCate()
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
	}
	.pics{
		display: flex;
		height: 100%;
		.left{
			width: 200rpx;
			height: 100%;
			border-right: 1px solid #eee;
			view{
				height: 60px;
				line-height: 60px;
				color: #333;
				text-align: center;
				font-size: 30rpx;
				border-top: 1px solid #eee;
			}
			.active{
				color: #fff;
				background-color: $shop-color;
			}
		}
		.right{
			width: 520rpx;
			height: 100%;
			margin: 20rpx auto;
			.item{
				border-bottom: 1px solid #eee;
				image{
					width: 520rpx;
					height: 600rpx;
					border-radius: 5px;
				}
				text{
					font-size: 30rpx;
					line-height: 60rpx;
				}
			}
		}
	}
	.isOver{
		width: 100%;
		height: 50px;
		line-height: 50px;
		text-align: center;
		background-color: #fff;
	}
</style>
