<template>
	<view class="container">
		<u-subsection :list="ordList" fontSiz='20px' :current="curNow" mode='button' activeColor='#d60000' @change="sectionChange">
		</u-subsection>
		<view class="goods" v-for="item in GoodList" :key="item.id">
			<view class="goods_top">
				<view class="top_left">
					<uni-icons type="shop-filled" size="20"></uni-icons>
					<u--text text="听雨的旗舰店"></u--text>
					<uni-icons type="forward" size="15" color="#7d7d7d"></uni-icons>
				</view>
				<view class="top_right">
					<u--text text="买家已付款" type="warning"></u--text>
				</view>
			</view>
			<view class="goods_body">
				<view class="body_left">
					<img :src="item.src"
						alt="">
				</view>
				<view class="body_right">
					<view class="row1">
						<p>{{item.title}}</p>
						<u--text mode="price" :text="item.pirce"></u--text>
					</view>
					<view class="row2">
						<u--text type="info" lines="1" :text="item.size"></u--text>
						<u--text type="info" text="x1"></u--text>
					</view>
					<view class="row3">
						<u--text type="warning" :text="item.time"></u--text>

					</view>
					<view></view>
				</view>
			</view>
			<view class="goods_bottom">
				<view class="txt">
					<text>含运费险服务 实付款￥{{item.pirce}}</text>
				</view>
				<view class="btn">
					<u-button type="primary"  size="small" :plain="true" shape="circle" text="查看物流"></u-button>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				ordList: ['全部', '代付款', '代发货', '待收货', '待评价'],
				curNow: 0,
				GoodList:[{id:1,src:'https://img.alicdn.com/imgextra/i2/3841319629/O1CN01ycM80O2L08OTLMeW3_!!0-item_pic.jpg_430x430q90.jpg', 
				title:'男士短袖t恤新款2022夏季宽松男生半袖潮牌潮流打底上衣炸街tb',size:'白色;XL[130-150斤]',pirce:'39.90',time:'06月26日 16:00前发货'},
				{id:2,src:'https://gd4.alicdn.com/imgextra/i2/1876461486/O1CN01G2X9tH1MqdJHkv2Vj_!!1876461486.jpg_400x400.jpg',
				title:'森马夏季运动短裤男士四五分裤速干透气大裤衩冰丝休闲大码沙滩裤',size:'灰色;XL[130-150斤]',pirce:'29.00',time:'06月26日 16:00前发货'},
				{id:3,src:'https://img.alicdn.com/imgextra/i4/747945455/O1CN01Od6eih1qARHxEf9ql_!!747945455.jpg_430x430q90.jpg',
				title:'男鞋2022新款夏季透气防臭网面运动网鞋百搭小白增高老爹ins潮鞋',size:'米色;42',pirce:'59.00',time:'06月26日 16:00前发货'},
				{id:4,src:'https://img.alicdn.com/imgextra/i1/2891705366/O1CN01t4Qx2p1pVfuieptXz_!!2891705366.jpg_430x430q90.jpg',
				title:'沙琪玛整箱年货坚果萨其马软糯早餐办公室零食休闲食品小吃糕点',size:'坚果黑糖沙琪玛【2斤装】',pirce:'16.9',time:'今天发货'},
				{id:5,src:'https://img.alicdn.com/imgextra/https://img.alicdn.com/imgextra/i1/217101303/O1CN01AxaqLh1LUopdNNz10_!!217101303.jpg_430x430q90.jpg',
				title:'宝洁海飞丝柔顺去屑洗发水液洗发露止痒清爽去油蓬松洗头发膏任选',size:'【男士专用】去屑洗发水730ml',pirce:'59.90',time:'06月26日 16:00前发货'},]
			};
		},
		methods: {
			sectionChange(index) {
				this.curNow = index;
			}
		},
	}
</script>

<style lang="scss">
	.container {
		background-color: #f0f0f0;
	}

	.goods {
		width: 95%;
		// height: 400rpx;	
		margin: 20rpx auto;
		padding: 20rpx 0;
		border-radius: 30rpx;
		background-color: #fff;

		.goods_top {
			display: flex;
			justify-content: space-between;
			align-items: center;
			margin: 10rpx auto;
			width: 95%;
			// height: 50rpx;

			.top_left {
				
				display: flex;
				align-items: center;
			}

			.top_right {}
		}

		.goods_body {
			display: flex;
			width: 95%;
			height: 200rpx;

			.body_left {
				width: 40%;
				height: 200rpx;
				margin-left: 20rpx;
				border-radius: 40rpx;
				overflow: hidden;

				img {
					width: 100%;
					height: 100%;
				}
			}

			.body_right {
				width: 100%;
				margin-left: 20rpx;
				height: 200rpx;

				.row1 {
					width: 100%;
					// height: 60rpx;
					display: flex;
					justify-content: space-between;
					align-items: center;

					p {
						width: 70%;
						height: 40rpx;
						overflow: hidden; //溢出隐藏    
						text-overflow: ellipsis; //文本显示省略号    /*默认是clip 超出部分直接切除*/
						whitewhite-space: nowrap; //不换行  /*默认normal 自动换行*/
						word-break: break-all;
					}
				}

				.row2 {
					display: flex;

					align-items: center;
					width: 100%;
					// height: 60rpx;

					p {
						width: 70%;
						height: 40rpx;
						overflow: hidden; //溢出隐藏    
						text-overflow: ellipsis; //文本显示省略号    /*默认是clip 超出部分直接切除*/
						whitewhite-space: nowrap; //不换行  /*默认normal 自动换行*/
						word-break: break-all;
					}
				}



			}
		

		}
		.goods_bottom {
			display: flex;
			flex-direction: column;
			align-items: flex-end;
			width: 100%;		
			.txt {
				// width: 100%;
				height: 50rpx;
				font-size: 12px;
				margin: 0 20rpx;
			}
			.btn {
				width: 200rpx;
				height: 50rpx;
				margin: 10rpx 20rpx;
			}
		}
	}
</style>
