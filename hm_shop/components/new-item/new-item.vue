<template>
	<view>
		<view class="news_item" @click="navigat(item.id)" v-for="item in list" :key="item.id">
			<image style="background-color: #FFECEC;" :src="item.img_url"></image>
			<view class="right">
				<view class="tit">
					{{item.title}}
				</view>
				<view class="info">
					<text>发表时间：{{item.add_time | formatDate}}</text>
					<text>浏览次数：{{item.click}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		},
		methods:{
			navigat(id){
				this.$emit('itemClick',id)
			}
		},
		props: ['list'],
		filters:{
			formatDate(date){
				const nDate = new Date(date)
				const year=nDate.getFullYear()
				const month=nDate.getMonth().toString().padStart(2,0)
				const day=nDate.getDay().toString().padStart(2,0)
				const str=[year,month,day].join("-")
				return str
			}
		}
	}
</script>

<style lang="scss">
	.news_item {
		display: flex;
		padding: 10rpx 20rpx;
		border-bottom: 1px solid $shop-color;

		image {
			min-width: 200rpx;
			max-width: 200rpx;
			height: 150rpx;
		}

		.right {
			margin-left: 15rpx;
			display: flex;
			flex-direction: column;
			justify-content: space-between;

			.tit {
				font-size: 30rpx;
			}

			.info {
				font-size: 24rpx;

				text:nth-child(2) {
					margin-left: 30rpx;
				}
			}
		}
	}
</style>
