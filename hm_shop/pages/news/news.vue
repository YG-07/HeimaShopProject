<template>
	<view class="news">
		<new-item @itemClick="goDetail" :list="newsList"></new-item>
	</view>
</template>

<script>
	import newItem from '../../components/new-item/new-item.vue'
	
	export default {
		data() {
			return {
				newsList:[]
			}
		},
		components:{
			newItem
		},
		methods: {
			// 获取新闻列表数据
			async getNews(){
				const res = await this.$myRuquest({
					url:'/api/getnewslist'
				})
				this.newsList = res.data.message
			},
			goDetail(id){
				uni.navigateTo({
					url:'/pages/news-detail/news-detail?id='+id
				})
			}
		},
		onLoad(){
			this.getNews()
		}
	}
</script>

<style>
</style>
