<template>
	<view class="home">
		<scroll-view scroll-x class="navscroll">
			<view class="item" 
			v-for="(item, index) in navArr"
			:class="index==navIndex ? 'active' : ''"
			@click="clickNav(index, item.id)"
			:key="item.id"
			>{{item.classname}}</view>
		</scroll-view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navIndex:0,
				navArr:[],
				newsArr:[],
				currentPage:1,
				currentId:50,
				loading:0       //0默认  1加载中  2没有更多了
			}
		},
		onLoad() {
			this.getNavData()
		},
		methods: {
			clickNav(index, id) {
				
			},
			getNavData() {
				uni.request({
					url:'https://ku.qingnian8.com/dataApi/news/navlist.php',
					success:res=>{
						console.log(res)
						this.navArr=res.data
					}
				})
			}
		}
	}
</script>

<style>
.navscroll {
	height: 100rpx;
	background: #F7F8FA;
	white-space: nowrap;
	position: fixed;
	left:0;
	top:var(--window-top);
	/deep/ ::-webkit-scrollbar {
		width: 4px !important;
		height: 1px !important;
		overflow: auto !important;
		background: transparent !important;
		-webkit-appearance: auto !important;
		display: block;
	}
	.item {
		font-size: 40rpx;
		display: inline-block;
		line-height: 100rpx;
		padding: 0 30rpx;
		color: #333;
		&.active {
			color: #c6aef1;
		}
	}
}
</style>
