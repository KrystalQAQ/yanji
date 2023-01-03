<template>
	<view class="content">
		<!-- <button @click="testco()">请求云对象的方法</button> -->

		<button class="sys_btn" open-type="getUserInfo" lang="zh_CN" @getuserinfo="appLoginWx">微信登录</button>

	</view>
</template>

<script>
	export default {
		data() {
			return {}
		},
		methods: {
			appLoginWx() {
				// #ifdef MP-WEIXIN
				uni.getProvider({
					service: 'oauth',
					success: function(res) {
						if (~res.provider.indexOf('weixin')) {
							uni.login({
			  			provider: 'weixin',
								success: (res2) => {
									let code=res2.code;
									let appid="wx5008d46116e464b1";
									let appSecret="ae03ad18f593c2c3940f3b6cee8035cb";
									let cs={
										"js_code":code,
										"appid":appid,
										"secret":appSecret,
										"grant_type":"authorization_code"
									}
									uni.request({
										url:"https://api.weixin.qq.com/sns/jscode2session",
										data:cs,
										success(res) {
											console.log("session_key",res.data.session_key)
											console.log("openid",res.data.openid)
										}
									})
									// uni.getUserInfo({
									// 	provider: 'weixin',
									// 	success: (info) => { //这里请求接口
									// 		console.log(res2);
									// 		console.log(info);

									// 	},
									// 	fail: () => {
									// 		uni.showToast({
									// 			title: "微信登录授权失败",
									// 			icon: "none"
									// 		});
									// 	}
									// })

								},
								fail: () => {
									uni.showToast({
										title: "微信登录授权失败",
										icon: "none"
									});
								}
							})

						} else {
							uni.showToast({
								title: '请先安装微信或升级版本',
								icon: "none"
							});
						}
					}
				});
				//#endif
			},

			async testco() { // 注意异步
				const helloco = uniCloud.importObject('login') // 导入云对象
				try {
					const res = await helloco; //导入云对象后就可以直接调用该对象的sum方法了，注意使用异步await
					console.log(res) // 结果是3
				} catch (e) {
					console.log(e)
				}
			}
		}
	}
</script>
