<template>
	<view class="container">

		<mySearch @click="goSearch()"></mySearch>

		<view class="scroll-view-container">
			<!-- 左侧的滚动视图区域 -->
			<scroll-view class="left-scroll-view" scroll-y>
				<view v-for="(item,i) in List" :key="i">
					<view :class="['left-scroll-view-item', i === active ? 'active' : '']" @click="activeChanged(i)">
						{{item.cat_name}}
					</view>
				</view>

			</scroll-view>
			<!-- 右侧的滚动视图区域 -->
			<scroll-view class="right-scroll-view" scroll-y :scroll-top="scrollTop">
				<view class="cate-lv2" v-for="(item2,i) in cateLevel2" :key="i">
					<view class="cate-lv2-title">{{item2.cat_name}}</view>
					<!-- 动态渲染三级分类的列表数据 -->
					<view class="cate-lv3-list">
						<!-- 三级分类 Item 项 -->
						<view class="cate-lv3-item" v-for="(item3, i3) in item2.children" :key="i3"
							@click="gotoGoodsList(item3)">
							<!-- 图片 -->
							<img :src="item3.cat_icon" alt="">
							<!-- 文本 -->
							<text>{{item3.cat_name}}</text>
						</view>
					</view>
				</view>

			</scroll-view>
		</view>

	</view>
</template>

<script>
	import badgeMix from '@/mixins/tabbar-badge.js'
	export default {
		  mixins: [badgeMix],
		data() {
			return {
				active: 0,
				// 一级列表的list
				List: [],
				// 二级列表的list
				cateLevel2: [],
				// 滚动条距离顶部的距离
				scrollTop: 0
			}


		},
		onLoad() {
			this.getList()
		},
		methods: {
			async getList() {
				// 发起请求
				const {
					data: res
				} = await uni.$http.get('/api/public/v1/categories')
				// 判断是否获取失败
				if (res.meta.status !== 200) return uni.$showMsg()
				// 转存数据
				// console.log("LIst" + res.message);
				this.List = res.message
				this.cateLevel2 = res.message[0].children

				// uni.request({
				// 	url: 'https://api-hmugo-web.itheima.net/api/public/v1/categories',
				// 	method: 'GET',
				// 	success: (res) => {
				// 		this.List = res.data.message
				// 		// console.log(this.List);
				// 		this.cateLevel2 = res.data.message[0].children
				// 		// console.log(this.cateLevel2);
				// 	}
				// })
			},
			activeChanged(i) {
				this.active = i
				this.cateLevel2 = this.List[i].children
				// 让 scrollTop 的值在 0 与 1 之间切换
				this.scrollTop = this.scrollTop === 0 ? 1 : 0
			},
			goSearch() {
				uni.navigateTo({
					url: '/pages/search/search'
				})
			},
			gotoGoodsList(item3) {
				// console.log(123);
				uni.navigateTo({
					url: '/pages/goods_list/goods_list?cid=' + item3.cat_id
				})
			}

		}
	}
</script>

<style lang="scss" scoped>
	.container {
		background-color: #ffffff;
	}

	.top_box {
		width: 100%;
		height: 100rpx;
		background-color: #d60000;

		.search {
			padding: 20rpx;
		}
	}

	.scroll-view-container {
		height: 100vh;
		display: flex;

		.left-scroll-view {
			width: 240rpx;

			.left-scroll-view-item {
				line-height: 120rpx;
				background-color: #f3f3f3;
				font-size: 24rpx;
				font-weight: bold;
				text-align: center;
				padding: 10rpx 0;

				// 激活项的样式
				&.active {
					background-color: #ffffff;
					position: relative;

					// 渲染激活项左侧的红色指示边线
					&::before {
						content: ' ';
						display: block;
						width: 6rpx;
						height: 60rpx;
						background-color: #c00000;
						position: absolute;
						left: 0;
						top: 50%;
						transform: translateY(-50%);
					}
				}
			}

		}

		.cate-lv2-title {
			font-size: 12px;
			font-weight: bold;
			text-align: center;
			padding: 15px 0;
		}

		.cate-lv3-list {
			display: flex;
			flex-wrap: wrap;

			.cate-lv3-item {
				width: 33%;
				margin-bottom: 10px;
				display: flex;
				flex-direction: column;
				align-items: center;

				img {
					width: 120rpx;
					height: 120rpx;
				}

				text {
					font-size: 24rpx;
				}
			}
		}
	}
</style>
