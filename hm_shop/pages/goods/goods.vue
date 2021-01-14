<template>
	<view class="goods">
		<goods-list :goods="goods"></goods-list>
		<view class="isOver" v-if="flag">
			-----我是有底线的-----
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
				pageindex:1,
				flag:false,
				goods:[]
			}
		},
		methods: {
			// 获取商品数据
			async getGoodsList(callBack){
				const res=await this.$myRuquest({
					url:'/api/getgoods?pageindex='+this.pageindex
				})
				// 保留之前的数据，展开数组并拼接
				this.goods=[...this.goods,...res.data.message]
				if(res.data.message.length<10)return this.flag=true
				callBack&&callBack()
			}
		},
		onLoad() {
			this.getGoodsList()
		},
		onReachBottom() {
			if(this.flag)return
			this.pageindex++
			this.getGoodsList()
		},
		onPullDownRefresh() {
			this.pageindex=1
			this.goods=[]
			this.flag=false
			setTimeout(()=>{
				this.getGoodsList(()=>{
					setTimeout(()=>{
						uni.stopPullDownRefresh()
					},400)
				})
			},600)
		}
	}
</script>

<style lang="scss">
	.goods{
		background-color: #eee;
	}
	.isOver{
		width: 100%;
		height: 50px;
		line-height: 50px;
		text-align: center;
		background-color: #fff;
	}
</style>
