<script>
	// 用户登录获取用户信息接口
	// import {
	// 	loginByAuth
	// } from '../../network/login/login.js';
	// //  用于获取用户的openid和sessionkey的接口
	// import {
	// 	jscode2session
	// } from '../../network/tripartite/tripartite.js'
	export default {
		data() {
			return {}
		},
		methods: {
			login() {
				// 调用wx的api显示登录中
				wx.showLoading({
			 	title: '登陆中',
				})
				// 调用uniapp的登录接口
				uni.login({
					success: async (res) => {
						if (res.errMsg == 'login:ok') {
// res.code用户登录凭证。开发者需要在开发者服务器后台，使用 code 换取 openid 和 session_key 等信息，微信登录配置onlyAuthorize:true才会返回
							const userOpenid = await jscode2session(res.code);
							//使用openid 获取用户的user信息，以及token信息
							const loginRes = await loginByAuth(userOpenid.data.data.openid);
							// 如果还没有登录注册过，返回的空数据
							if (JSON.stringify(loginRes.data.data) === "{}") {
								//! 传递openid参数给【注册】界面
								let params = {
									openid: userOpenid.data.data.openid
								}
								console.log("用户信息不存在", params)
								wx.hideLoading()
								// 跳转到注册页面，注册用户信息
								uni.navigateTo({
									url: '../register/register?user=' + JSON.stringify(params)
								})
							} else {
								// 如果用户登录过，返回来用户信息，保存用户信息以及token在user变量当中
								let user = {
									...loginRes.data.data.user,
									token: loginRes.data.data.token
								};
								// 保存用户数据在本地
								uni.setStorageSync("wxuser", user);
								// 调用wx的api关闭登录中
								wx.hideLoading();
								// 登录后跳转到用户页面
								uni.switchTab({
									url: "../../pages/user/user"
								})
							}
						}
					}
				})
			}
		},
	}
</script>