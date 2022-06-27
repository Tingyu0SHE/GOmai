<template>
	<view class="container">
		<!-- 搜索框 -->
		<view class="box" @click="goSearch()">
			<u-search placeholder="请输入内容" :showAction="false"></u-search>
			<!-- <mySearch></mySearch> -->
		</view>
		<!-- 轮播图 -->
		<view class="swiper" @click="gotoGoodsList" >
			<u-swiper :list="list2" indicator indicatorMode="line" height="150" keyName="image" circular></u-swiper>
		</view>
		<!-- nav导航栏 -->
		<view class="switch">
			<!-- 导航栏切换 -->
			<view class="title">
				<view class="min" v-for="item in ListT" :key="item.id" :class="{'active':acId==item.id}"
					@click="tiggle(item.id)">
					{{item.name}}
				</view>
			</view>
			<!-- 内容区域 -->
			<view class="footer">
				<!-- 分类模块 -->
				<view v-if="acId==1">
					<view class="head" v-for="(item,index) in itemList" :key="index">
						<!-- 标题 -->
						<view class="pic">
							<img :src="item.floor_title.image_src" alt="">
						</view>
						<!-- 里面的图片 -->
						<view class="head_body">
							<!-- 左边的大图 -->
							<view class="body_left" @click="gotoGoodsList">
								<img :src="item.product_list[0].image_src" alt="">
							</view>
							<!-- 右边四个小图 -->
							<view class="body_right" @click="gotoGoodsList">
								<view class="four_pic" v-for="(item2, i2) in item.product_list" :key="i2"
									v-if="i2 !== 0">
									<img :src="item2.image_src">
								</view>
							</view>
						</view>
					</view>

				</view>
				<!-- 秒杀区域 -->
				<view v-else-if="acId==2">
					<view class="Best_Sellers" v-for="item in msList" :key="item.id">
						<!-- 图片区域 -->
						<view class="best_pic">
							<img :src="item.src" alt="">
						</view>
						<!-- 进度条 -->
						<view class="artb">
							<p>{{item.title}}</p>
							<view style="margin: 10rpx 0;">
								<u-line-progress :percentage="item.Percent" activeColor="#d60000"></u-line-progress>
							</view>
							<view style="width: 180rpx;margin-top: 10rpx;  font-size:20rpx">
								<u-tag text="30天保价" type="error"></u-tag>
							</view>
							<view class="bttom_btn">
								<p>￥{{item.pirce}}</p>
								<button>抢购</button>
							</view>
						</view>
					</view>
				</view>
				<view v-else-if="acId==3">
					<u-sticky bgColor="#fff">
						<u-tabs :list="list1"></u-tabs>
					</u-sticky>

					<view class="sup_market" v-for="item in markList" :key="item.id">
						<!-- 图片区域 -->
						<view class="sup_img">
							<img :src="item.src" alt="">
						</view>
						<view class="txt_body">
							<p>{{item.title}}</p>
							<!-- 好评距离模块 -->
							<view style="width: 100%; height: 30rpx;margin-top: 20rpx; display: flex;">
								<!-- 五星好评的星星 -->
								<view style="width: 30rpx; height: 100%;margin-right: 10rpx;">
									<img src="/static/xing.png" alt="" style="width: 100%; height: 100%;">
								</view>
								<!-- 五星数量 -->
								<view>{{item.Grade}}</view>
								<!-- 月销 -->
								<view style="margin-left: 20rpx;">月销{{item.sales}}</view>
								<!-- 距离时间 -->
								<view style="margin-left: 80rpx;">{{item.time}}分钟</view>
								<!-- 距离 -->
								<view style="margin-left: 20rpx;">{{item.km}}km</view>
								
							</view>
							<!-- 起送 -->
							<view style="margin-top: 20rpx;">
								起送￥{{item.Start}} &nbsp;&nbsp;&nbsp;{{item.Distribution}}
							</view>
							<view style="color: #d60000; border: 1px solid #d60000; width: 75%;
							margin-top: 10rpx;
							border-radius: 10rpx;
							 padding:0 5rpx;text-align: center;">
								满21减20|满55减23|满60减20
							</view>
						</view>
					</view>
				</view>
			</view>

		</view>
	</view>
	</view>
</template>

<script>
	import badgeMix from '@/mixins/tabbar-badge.js'
	export default {
		mixins: [badgeMix],
		data() {
			return {
				acId: 1,
				scrollTop: 0,
				list2: [{
					image: 'https://cdn.uviewui.com/uview/swiper/swiper2.png',
				}, {
					image: 'https://cdn.uviewui.com/uview/swiper/swiper1.png',
				}, {
					image: 'https://cdn.uviewui.com/uview/swiper/swiper3.png',
				}],
				ListT: [{
						id: 1,
						name: '分类'
					},
					{
						id: 2,
						name: '秒杀价'
					},
					{
						id: 3,
						name: '超市购物'
					}
				],
				text1: 'uView UI众多组件覆盖开发过程的各个需求，组件功能丰富，多端兼容。让您快速集成，开箱即用',
				msList: [{
						id: 1,
						title: '改良旗袍连衣裙2022新款春夏季女高端品牌洋气质两件套装',
						Percent: 99,
						pirce: 159,
						src: "https://img.alicdn.com/imgextra/i4/839750895/O1CN01T764N31ITxE22wnSx_!!0-item_pic.jpg_430x430q90.jpg"
					},
					{
						id: 2,
						title: '回力男鞋夏季透气2022新款网面运动鞋潮流跑步老爹鞋',
						Percent: 60,
						pirce: 241,
						src: "https://img.alicdn.com/imgextra/i1/3430463052/O1CN01pFMOlO1YPrXSSIrop_!!3430463052.jpg_430x430q90.jpg"
					},
					{
						id: 3,
						title: '冰丝牛仔裤男夏季薄款潮牌宽松哈伦束脚工装',
						Percent: 50,
						pirce: 79,
						src: "https://img.alicdn.com/imgextra/https://img.alicdn.com/imgextra/i1/2095559545/O1CN01mIq7Kq2KNfBwlnfPs_!!2095559545.jpg_430x430q90.jpg"
					},
					{
						id: 4,
						title: '海飞丝控油去屑洗发水止痒洗发露清爽蓬松去油洗头膏官方正品',
						Percent: 80,
						pirce: 59,
						src: "https://img.alicdn.com/imgextra/https://img.alicdn.com/imgextra/i1/217101303/O1CN01HPHBXr1LUopuZl5N9_!!217101303.jpg_430x430q90.jpg"
					},
					{
						id: 5,
						title: '木糖醇山药桃酥老式正宗铁棍零食无蔗糖独立包装桃酥饼干',
						Percent: 90,
						pirce: 39,
						src: "https://img.alicdn.com/imgextra/i4/2212731552099/O1CN01M6QY6J1RNO5fFwBgI_!!2212731552099.jpg_430x430q90.jpg	"
					},
					{
						id: 6,
						title: '支持鸿᷂星᷂尔᷂克2022夏新款短袖t恤男士ins潮牌半袖冰丝',
						Percent: 99,
						pirce: 59,
						src: "https://gd2.alicdn.com/imgextra/i4/831688642/O1CN0169hGsx2Di5Y74f0iK_!!831688642.jpg_400x400.jpg"
					},
				],
				itemList: [{
						"floor_title": {
							"name": "时尚女装",
							"image_src": "http://210.21.98.31:6005/pyg/pic_floor01_title.png"
						},
						"product_list": [{
								"name": "优质服饰",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor01_1@2x.png",
								"image_width": "232",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=服饰"
							},
							{
								"name": "春季热门",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor01_2@2x.png",
								"image_width": "233",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=热"
							},
							{
								"name": "爆款清仓",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor01_3@2x.png",
								"image_width": "233",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=爆款"
							},
							{
								"name": "倒春寒",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor01_4@2x.png",
								"image_width": "233",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=春季"
							},
							{
								"name": "怦然心动",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor01_5@2x.png",
								"image_width": "233",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=心动"
							}
						]
					},
					{
						"floor_title": {
							"name": "户外活动",
							"image_src": "http://210.21.98.31:6005/pyg/pic_floor02_title.png"
						},
						"product_list": [{
								"name": "勇往直前",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor02_1@2x.png",
								"image_width": "232",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=户外"
							},
							{
								"name": "户外登山包",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor02_2@2x.png",
								"image_width": "273",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=登山包"
							},
							{
								"name": "超强手套",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor02_3@2x.png",
								"image_width": "193",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=手套"
							},
							{
								"name": "户外运动鞋",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor02_4@2x.png",
								"image_width": "193",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=运动鞋"
							},
							{
								"name": "冲锋衣系列",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor02_5@2x.png",
								"image_width": "273",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=冲锋衣"
							}
						]
					},
					{
						"floor_title": {
							"name": "箱包配饰",
							"image_src": "http://210.21.98.31:6005/pyg/pic_floor03_title.png"
						},
						"product_list": [{
								"name": "清新气质",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor03_1@2x.png",
								"image_width": "232",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=饰品"
							},
							{
								"name": "复古胸针",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor03_2@2x.png",
								"image_width": "263",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=胸针"
							},
							{
								"name": "韩版手链",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor03_3@2x.png",
								"image_width": "203",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=手链"
							},
							{
								"name": "水晶项链",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor03_4@2x.png",
								"image_width": "193",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=水晶项链"
							},
							{
								"name": "情侣表",
								"image_src": "http://210.21.98.31:6005/pyg/pic_floor03_5@2x.png",
								"image_width": "273",
								"open_type": "navigate",
								"navigator_url": "/pages/goods_list?query=情侣表"
							}
						]
					}


				],
				list1: [{
					name: '综合排序',
				}, {
					name: '销量高',
					badge: {
						isDot: true
					}
				}, {
					name: '速度快',
					badge: {
						value: 5,
					}
				}, {
					name: '距离近'
				}, {
					name: '津贴优惠'
				}],
				markList: [{
						id: 1,
						src: "https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg.yunhuzx.com%2Ffiles%2Fuploads%2F2019%2F08-18%2F156609613137eed0742066.jpg&refer=http%3A%2F%2Fimg.yunhuzx.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1657968648&t=217b30ce66f73e2282890c7850e693d3",
						title: '家佳超市',
						km: 5.8,
						time: 15,
						Grade: 5,
						sales: 351,
						Start: 12,
						Distribution: '免配送费'

					},
					{
						id: 2,
						src: "https://img1.baidu.com/it/u=901009453,1581087377&fm=253&fmt=auto&app=138&f=JPEG?w=532&h=500",
						title: '阳光超市',
						km: 6.2,
						time: 29,
						Grade: 5,
						sales: 6425,
						Start: 12,
						Distribution: '免配送费'
					},
					{
						id: 3,
						src: "https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fwww.logo123.net%2Flogos%2F2014%2F03%2F24%2F2014032409013010100.jpg&refer=http%3A%2F%2Fwww.logo123.net&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1657968804&t=7b9b3720fb5c2f60cd9480b37479a1fc",
						title: '市民超市',
						km: 5.4,
						time: 52,
						Grade: 5,
						sales: 254,
						Start: 12,
						Distribution: '配送6'
					},
					{
						id: 4,
						src: "https://img2.baidu.com/it/u=1095704739,1758037331&fm=253&fmt=auto&app=120&f=JPEG?w=500&h=354",
						title: '全民超市',
						km: 10.6,
						time: 30,
						Grade: 5,
						sales: 845,
						Start: 12,
						Distribution: '配送￥5'
					},
					{
						id: 5,
						src: "https://img0.baidu.com/it/u=4291738693,1525607317&fm=253&fmt=auto&app=138&f=JPEG?w=709&h=473",
						title: '新百顺精品超市',
						km: 20.5,
						time: 45,
						Grade: 5,
						sales: 568,
						Start: 12,
						Distribution: '免配送费'
					},
				]
			}
		},
		onLoad() {
			this.getList()
		},
		methods: {
			getList() {
				uni.request({
					url: 'https://api-hmugo-web.itheima.net/api/public/v1/home/floordata',
					method: 'GET',
					success: (res) => {
						this.itemList = res.data.message
						// console.log("首页"+this.itemList);
					}

				})
			},
			tiggle(id) {
				// console.log(123);
				this.acId = id;
			},
			// 点击搜素前往搜索界面
			goSearch() {
				uni.navigateTo({
					url: '/pages/search/search'
				})
			},
			gotoGoodsList() {
				uni.navigateTo({
					url: '/pages/goods_list/goods_list'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	@import "uview-ui/index.scss";

	.box {
		position: sticky;
		top: 0;
		z-index: 999;
		width: 95%;
		margin: 0 auto;
		padding: 20rpx;
		background-color: #d60000;

	}

	.swiper {
		width: 100%;
		height: 300rpx;
		background-color: #d60000;
	}

	.switch {
		width: 94%;
		height: 100rpx;
		padding: 10rpx 20rpx;

		.title {
			display: flex;
			justify-content: space-around;
			width: 100%;
			height: 110rpx;
			color: #797677;
			font-size: 32rpx;

			.min {
				width: 33%;
				height: 100%;
				text-align: center;
				line-height: 100rpx;
				font-weight: 700;
				
			}

			.active {
				background-color: #d60000;
				font-size: 40rpx;
				color: #fff;
			}
		}

		// 滚动条
		.footer {
			height: 300rpx;
			width: 100%;

			.head {
				margin-top: 10rpx;
				width: 100%;

				.pic {
					width: 100%;
					height: 60rpx;

					img {
						width: 100%;
						height: 100%;
					}
				}

				.head_body {
					width: 100%;
					height: 400rpx;
					display: flex;

					.body_left {
						width: 40%;
						height: 100%;

						img {
							width: 100%;
							height: 100%;
						}
					}

					.body_right {
						display: flex;
						flex-wrap: wrap;
						width: 60%;
						height: 100%;

						.four_pic {
							width: 45%;
							height: 45%;
							padding: 10rpx;

							img {
								width: 100%;
								height: 100%;
							}
						}
					}
				}
			}

			.Best_Sellers,
			.sup_market {
				display: flex;
				width: 100%;
				height: 250rpx;
				margin-top: 10rpx;
				border-radius: 10rpx;
				background-color: #e6e6e6;

				.best_pic,
				.sup_img {
					width: 30%;
					height: 200rpx;
					margin: 20rpx 20rpx;
					background-color: #d60000;
					border-radius: 20rpx;
					overflow: hidden;

					img {

						width: 100%;
						height: 100%;
					}
				}

				.artb,
				.txt_body {
					width: 70%;
					height: 200rpx;
					margin: 10rpx 0;
					font-size: 12px;

					p {
						font-weight: 700;
						font-size: 36rpx;
						white-space: nowrap;
						overflow: hidden;
						text-overflow: ellipsis;
					}

					.bttom_btn {
						// margin-top: 20rpx;
						display: flex;
						justify-content: space-between;

						p {
							color: #d60000;
							font-weight: 700;
							font-size: 32rpx;
						}

						button {
							background-color: #d60000;
							color: #fff;
							line-height: 50rpx;
							font-size: 24rpx;
							width: 150rpx;
							height: 50rpx;
						}
					}
				}
			}

			// .sup_market {
			// 	display: flex;
			// 	width: 100%;
			// 	height: 250rpx;
			// 	background-color: #797677;
			// 	margin-top: 10rpx;
			// 	border-radius: 10rpx;
			// 	.sup_img {
			// 		width: 30%;
			// 		height: 200rpx;
			// 		margin: 20rpx 20rpx;
			// 		background-color: #d60000;
			// 	}
			// }

		}

	}
</style>
