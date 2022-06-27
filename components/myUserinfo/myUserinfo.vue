<template>
	<view>
		<view class="user_top">
			<view class="left">
				<u-icon size="50" name="/static/business.png"></u-icon>
				<p>认证商家</p>
			</view>
			<view class="middle">
				<u-avatar :src="userinfo.avatarUrl" shape="circle" size="90"></u-avatar>
				<p>{{userinfo.nickName}}</p>
			</view>
			<view class="right" @click="num++">
				<u-icon size="50" name="/static/goods.png"></u-icon>
				<p>{{num}}赞</p>
			</view>
		</view>
		<view class="user_body">
			<u-grid :border="false" col="5" style="width: 100%;">
				<u-grid-item style="width: 20%;border-right: 2rpx solid #e9e9e9;" v-for="(listItem,listIndex) in MList"
					:key="listIndex" @click="gotoOrder(listIndex)">
					<u-icon :customStyle="{paddingTop:30+'rpx'}" :name="listItem.name" size="35"></u-icon>
					<text class="grid-text" style="font-size: 28rpx;">{{listItem.title}}</text>
				</u-grid-item>
			</u-grid>
		</view>
		<view class="user_list">
			<u-cell-group title-bg-color="rgb(243, 244, 246)">
				<u-cell :titleStyle="{fontWeight: 600}" :title="item.title" v-for="(item, index) in fList" :key="index"
					isLink :icon="item.iconUrl" style="height: 90rpx;" @click="logout(index)">
				</u-cell>
			</u-cell-group>
		</view>
	</view>
	</view>
</template>

<script>
	import {
		mapState,
		mapMutations
	} from "vuex"
	export default {
		name: "myUserinfo",
		data() {
			return {
				num: 0,
				MList: [{
					name: 'calendar',
					title: '代付款'
				}, {
					name: 'car',
					title: '待收货'
				}, {
					name: 'rmb-circle',
					title: '退款/退货'
				}, {
					name: 'order',
					title: '全部订单'
				}, {
					name: 'chat',
					title: '全部评价'
				}],
				fList: [{
					title: '我的商城',
					iconUrl: '/static/shop.png'
				}, {
					title: '收货地址',
					iconUrl: '/static/adress.png'
				}, {
					title: '店铺会员',
					iconUrl: '/static/vip.png'
				}, {
					title: '我的快递',
					iconUrl: '/static/kuaidi.png'
				}, {
					title: '联系我们',
					iconUrl: '/static/laixnxi.png'
				}, {
					title: '退出登录',
					iconUrl: '/static/logout.png'
				}, {
					title: '设置',
					iconUrl: '/static/setup.png'
				}]
			};
		},
		computed: {
			...mapState('m_user', ['userinfo'])
		},
		methods: {
			...mapMutations('m_user', ['updateUserInfo', 'updateToken', 'updateAddress']),
			async logout(i) {
				if (i == 5) {
					// 询问用户是否退出登录
					// console.log(11111);
					const [err, succ] = await uni.showModal({
						title: '提示',
						content: '确认退出登录吗？'
					}).catch(err => err)

					if (succ && succ.confirm) {
						// 用户确认了退出登录的操作
						// 需要清空 vuex 中的 userinfo、token 和 address
						this.updateUserInfo({})
						this.updateToken('')
						this.updateAddress({})
					}
				} else if (i == 4) {
					uni.showModal({
						title: '提示',
						content: '是否要拨打电话+18660849725？',
						success:(res)=>{
							if (res.confirm) {
								// console.log('comfirm') //点击确定之后执行的代码
								uni.makePhoneCall({
									phoneNumber: '18660849725' //仅为示例
								});
							}
						}
					})
					
				}
			},
			gotoOrder(i) {
				console.log(132);
				if (i + 1) {
					uni.navigateTo({
						url: '/pages/order/order'
					})
				}
			}

		},
		// 点击订单跳转到组件里面
		// 根据订单的索引跳转到对应的页面
	

	}
	
</script>

<style lang="scss">
	* {
		margin: 0;
		padding: 0;
	}

	.container {
		background-color: #f0eff4;

	}

	.user_top {
		display: flex;
		justify-content: space-around;
		align-items: center;
		width: 100%;
		height: 400rpx;
		background-color: #d60000;

		.left,
		.middle,
		.right {
			width: 30%;
			height: 300rpx;
			display: flex;
			flex-direction: column;
			align-items: center;

			p {
				color: #fff;
			}
		}

		.left {
			justify-content: center;

			p {
				margin-top: 10rpx;
				font-size: 24rpx;
			}
		}

		.middle {
			justify-content: space-around;

			p {
				font-size: 32rpx;
			}
		}

		.right {
			justify-content: center;

			p {
				margin-top: 10rpx;
				font-size: 24rpx;
			}
		}
	}

	.user_body {
		display: flex;
		width: 100%;
		height: 200rpx;
		margin-top: 40rpx;
		background-color: #fff;

	}

	.user_list {
		width: 100%;

		margin-top: 60rpx;
		background-color: #fff;
	}
</style>
