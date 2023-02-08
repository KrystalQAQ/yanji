<template>
	<view class="content">
		<view class="flex padding justify-center">
			{{nickName}}
			<button class="cu-btn round bg-red" @click="getUserInfo">立即登录</button>
			<!-- <button class="cu-btn round bg-red" @click="tz">跳转</button> -->
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				nickName: ""
			}
		},
		methods: {
			tz() {
				uni.redirectTo({
					url: '/pages/index/index'
				});
				// uni.switchTab({
				// 	url: '/pages/zy/zy'
				// });
			},
			getUserInfo() {
				const _this = this
				uni.getUserProfile({
					desc: '用于完善会员资料',
					success: (result) => {
						_this.userInfo = result.userInfo
						_this.nickName = result.userInfo.nickName
						_this.wxLogin()
					},
					fail: () => {
						uni.hideLoading();
						uni.showModal({
							content: '获取用户信息失败',
							showCancel: false
						})
					}
				})
			},

			wxLogin() {
				const _this = this
				uni.showLoading({
					title: '加载中'
				});

				uni.login({
					provider: 'weixin',
					success: (res) => { // 获取 code
						// console.log(_this.userInfo)
						if (res.code) {
							uniCloud.callFunction({
								name: 'user',
								data: {
									action: 'code2Session',
									js_code: res.code,
									user_info: _this.userInfo
								},
								success: (res) => {
									// _this.nickName=res.result
									uni.showToast({
										title: '登录成功',
										// icon :"fail"
									})
									// _this.tz()
									console.log('mp_wx_openid', res.result.result.result
										.mp_wx_openid)

									console.log('_id', res.result.result.result)
									try {
										uni.setStorageSync('mp_wx_openid', JSON.stringify(res.result.result.result));
									} catch (e) {
										// error
										uni.showToast({
											title: e,
											// icon :"fail"
										})
									}
									_this.tz()
									// console.log('nickName', res.result.result.result.nickName)

									// uni.hideLoading();
									// if (res.result.result.result._id) {
									// 	uni.setStorageSync('userInfo', JSON.stringify(res.result
									// 		.result.result))
									// 	globalData.$UserInfo = res.result.result.result
									// }
								},
								fail: () => {
									uni.hideLoading();
									uni.showToast({
										title: '云函数调用失败',
										icon: "fail"
									})
									// console.log('云函数调用失败')
								}
							})
						}
					}
				})
			}
		},
	}
</script>
