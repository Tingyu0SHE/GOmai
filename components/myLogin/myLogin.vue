<template>
	<view class="login-container">
		<!-- 提示登录的图标 -->
		<uni-icons type="contact-filled" size="100" color="#AFAFAF"></uni-icons>
		<!-- 登录按钮 -->
		<!-- open-type="getUserInfo" @getuserinfo="getUserInfo" -->
		<button type="primary" class="btn-login" @tap="getUserProfile">一键登录</button>
		<!-- 登录提示 -->
		<view class="tips-text">登录后尽享更多权益</view>
	</view>
</template>

<script>
	import {
		mapMutations,
		mapState
	} from 'vuex'
	export default {
		name: "myLogin",
		data() {
			return {

			};
		},
		computed: {
			...mapState('m_user', ['redirectInfo']),
		},
		methods: {
			...mapMutations('m_user', ['updateUserInfo', 'updateToken', 'updateRedirectInfo']),
			getUserProfile(e) {
				wx.getUserProfile({
					desc: '用于完善会员资料', // 声明获取用户个人信息后的用途，后续会展示在弹窗中，请谨慎填写
					success: (res) => {
						// console.log(res);
						this.updateUserInfo(res.userInfo)
						this.getToken(res)
					},
					fail() {
						uni.$showMsg('您取消了登录授权！')
					}
				})
			},
			// 获取微信用户的基本信息
			// getUserInfo(e) {
			// 	// console.log(e);
			// 	// 判断是否获取用户信息成功
			// 	if (e.detail.errMsg === 'getUserInfo:fail auth deny') return uni.$showMsg('您取消了登录授权！')
			// 	// console.log("info"+e.detail.userInfo);  
			// 	// 获取用户信息成功， e.detail.userInfo 就是用户的基本信息

			// 	// 3. 将用户的基本信息存储到 vuex 中
			// 	this.updateUserInfo(e.detail.userInfo)

			// 	// console.log(111111);
			// 	// 获取登录成功后的 Token 字符串
			// 	this.getToken(e.detail)
			// },

			async getToken(info) {
				// 调用微信登录接口
				const [err, res] = await uni.login().catch(err => err)
				// console.log(res.errMsg);
				// console.log(err);

				// 判断是否 uni.login() 调用失败
				if (err || res.errMsg !== 'login:ok') return uni.$showMsg('登录失败')
				// uni.$showMsg('登录成功')

				// 准备参数对象
				const query = {
					code: res.code,
					encryptedData: info.encryptedData,
					iv: info.iv,
					rawData: info.rawData,
					signature: info.signature
				}
				// console.log(query.rawData);

				// 换取 token
				const loginResult = {
					"message": {
						"user_id": 23,
						"user_email_code": null,
						"is_active": null,
						"user_sex": "男",
						"user_qq": "",
						"user_tel": "",
						"user_xueli": "本科",
						"user_hobby": "",
						"user_introduce": null,
						"create_time": 1562221487,
						"update_time": 1562221487,
						"token": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOjIzLCJpYXQiOjE1NjQ3MzAwNzksImV4cCI6MTAwMTU2NDczMDA3OH0.YPt-XeLnjV-_1ITaXGY2FhxmCe4NvXuRnRB8OMCfnPo"
					},
					"meta": {
						"msg": "登录成功",
						"status": 200
					}
				}

				if (loginResult.meta.status !== 200) return uni.$showMsg('登录成功')
				// uni.$showMsg('登录成功')
				// 2. 更新 vuex 中的 token
				this.updateToken(loginResult.message.token)
				this.navigateBack()
			},
			// 返回登录之前的页面
			navigateBack() {
			  // redirectInfo 不为 null，并且导航方式为 switchTab
			  if (this.redirectInfo && this.redirectInfo.openType === 'switchTab') {
			    // 调用小程序提供的 uni.switchTab() API 进行页面的导航
			    uni.switchTab({
			      // 要导航到的页面地址
			      url: this.redirectInfo.from,
			      // 导航成功之后，把 vuex 中的 redirectInfo 对象重置为 null
			      complete: () => {
			        this.updateRedirectInfo(null)
			      }
			    })
			  }
			}
		}
	}
</script>

<style lang="scss">
	.login-container {
		// 登录盒子的样式
		height: 750rpx;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		background-color: #f8f8f8;
		position: relative;
		overflow: hidden;

		// 登录按钮的样式
		.btn-login {
			width: 90%;
			border-radius: 100px;
			margin: 15px 0;
			background-color: #c00000;
		}

		// 按钮下方提示消息的样式
		.tips-text {
			font-size: 12px;
			color: gray;
		}
	}
</style>
