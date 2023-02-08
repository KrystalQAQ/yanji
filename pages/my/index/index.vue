<template>
	<view>
		<view class="my-headbox">
			<view class="my-head">
				<view bindtap="goPage" class="v2" data-target="blank" data-url="/pages/my/grade/grade">
					<image class="img2" mode="widthFix" src="{{userInfo.gradeImg}}"></image>
				</view>
				<view bindtap="onGotUserInfo" class="my-getuserinfo">
					<image class="img1" mode="aspectFit"
						:src="avatarUrl">
					</image>
					<view class="v1">
						<text class="t1">{{userInfo.nickName}}</text>
						<view class="t4">
							<text class="t2">点击同步头像昵称</text>
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="my-numbox">
			<view bindtap="goPage" class="nlist" data-target="blank" data-url="/pages/my/daka/daka">
				<view class="n">
					{{10}}
					<text class="t1">天</text>
				</view>
				<view class="t">已加入</view>
			</view>
			<view bindtap="goPage" class="nlist" data-target="blank" data-url="/pages/my/daka/daka">
				<view class="n">
					{{20}}
					<text class="t1">笔</text>
				</view>
				<view class="t">已记账</view>
			</view>
			<view bindtap="goPage" class="nlist" data-target="blank" data-url="/pages/my/grade/grade">
				<view class="n">{{30}}</view>
				<view class="t">经验</view>
			</view>
		</view>
		<view class="eventsbox" wx:if="{{events.length>0}}">
			<scroll-view scrollX class="eventsboxscroll2">
				<view class="eventlist">
					<view class="evt" wx:for="{{events}}">
						<image bindtap="goPage" class="img1" data-target="blank" data-url="{{item.url}}"
							mode="heightFix" src="{{item.imgsrc}}"></image>
					</view>
					<view class="evt">
						<view class="more">更多活动敬请期待</view>
					</view>
				</view>
			</scroll-view>
		</view>
		<view class="line line2"></view>
		<view class="lists bgfboder">
			<view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/list/list">
				<view class="d1">
					<view class="d2"></view>
					<image class="img1" mode="widthFix" src="/static/10.png"></image>
					我的账本
				</view>
			</view>
			<view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/vip/open"
				wx:if="{{version.envVersion=='release'}}">
				<view class="d1">
					<view class="d2 c_red">{{viptip}}</view>
					<image class="img1" mode="widthFix" src="/static/36.png"></image>
					开通VIP
				</view>
			</view>
		</view>
		<view class="line line2"></view>
		<view class="lists bgfboder">
			<view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/my/settime/settime">
				<view class="d1">
					<view class="d2"></view>
					<image class="img1" mode="widthFix" src="/static/19.png"></image>
					定时提醒
				</view>
			</view>
			<view class="listr">
				<view class="d1">
					<view class="d2">{{userInfo.tel==''?'绑定手机防丢账':userInfo.tel}}</view>
					<image class="img1" mode="widthFix" src="/static/34.png"></image>
					绑定手机号
					<button bindgetphonenumber="getPhoneNumber" class="f_button" openType="getPhoneNumber"></button>
				</view>
			</view>
			<view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/my/password/password">
				<view class="d1">
					<view class="d2">{{userInfo.password!=''?'已开启':''}}</view>
					<image class="img1" mode="widthFix" src="/static/30.png"></image>
					密码保护
				</view>
			</view>
			<view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/my/excel/excel">
				<view class="d1">
					<view class="d2"></view>
					<image class="img1" mode="widthFix" src="/static/28.png"></image>
					导出表格
				</view>
			</view>
			<view bindtap="goPage" class="listr" data-target="blank"
				data-url="/pages/book/flag/list?bookid={{nowbookid}}">
				<view class="d1">
					<view class="d2"></view>
					<image class="img1" mode="widthFix" src="/static/39.png"></image>
					预算&目标
				</view>
			</view>
			<view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/img/img">
				<view class="d1">
					<view class="d2"></view>
					<image class="img1" mode="widthFix" src="/static/37.png"></image>
					账本图片管理
				</view>
			</view>
			<view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/my/account/account"
				wx:if="{{nowbook.BookAccount&&nowbook.BookAccount==0}}">
				<view class="d1">
					<view class="d2"></view>
					<image class="img1" mode="widthFix" src="/static/12.png"></image>
					我的资金账户(银行卡)
				</view>
			</view>
			<view bindtap="goPage" class="listr" data-target="blank"
				data-url="/pages/book/account/account?bookid={{nowbook.ID}}"
				wx:if="{{nowbook.BookAccount&&nowbook.BookAccount==1}}">
				<view class="d1">
					<view class="d2"></view>
					<image class="img1" mode="widthFix" src="/static/12.png"></image>
					账本资金账户(银行卡)
				</view>
			</view>
			<view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/my/plus/plus?type=1"
				wx:if="{{userInfo.id<106800}}">
				<view class="d1">
					<view class="d2"></view>
					<image class="img1" mode="widthFix" src="/static/8.png"></image>
					我的收入条目
				</view>
			</view>
			<view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/my/plus/plus?type=0"
				wx:if="{{userInfo.id<106800}}">
				<view class="d1">
					<view class="d2"></view>
					<image class="img1" mode="widthFix" src="/static/9.png"></image>
					我的支出条目
				</view>
			</view>
		</view>
		<view class="line line2"></view>

		<view class="tj-box-h"></view>

		<view class="share-bg" wx:if="{{shareShow==1}}">
			<view class="share-box">
				<view class="share-icon">
					<view class="share-list">
						<image class="img1" mode="widthFix" src="/static/24.png"></image>
						<view class="share-text">微信好友</view>
						<button bindtap="shareShow" class="share-button" openType="share"></button>
					</view>
					<view bindtap="goShowImg" class="share-list"
						data-src="https://static-1253713495.file.myqcloud.com/miniapps/jizhang/static/4.jpg">
						<image class="img1" mode="widthFix" src="/static/25.png"></image>
						<view class="share-text">发朋友圈</view>
					</view>
				</view>
				<view bindtap="shareShow" class="share-reset">取消</view>
			</view>
		</view>

	</view>
</template>
<script>
	export default {
		data() {
			return {
				avatarUrl:"",
				nickName: "",
				userInfo: {
					joinDay: "*",
					listCount: "*",
					integral: "*"
				},
				shareShow: 0,
				zhibo: {
					status: 1
				},
				viptip: "",
				nowbookid: 0,
				nowbook: {},

			}
		},
		onLoad() {
			try {
				const value = uni.getStorageSync('mp_wx_openid');
				var mp_wx_openid = JSON.parse(value).mp_wx_openid
				if (JSON.parse(value).mp_wx_openid) {
					this.avatarUrl = JSON.parse(value).avatarUrl
					// console.log(mp_wx_openid);
				} else {
					uni.showToast({
						title: '请先登录',
						icon: "fail"
					})
					uni.redirectTo({
						url: '/pages/login/login'
					});
				}
			} catch (e) {
				// error
				console.log("未登录", e);
				uni.showToast({
					title: '请先登录',
					icon: "fail"
				})
				uni.redirectTo({
					url: '/pages/login/login'
				});
			}
		},
		methods: {

		},
	}
</script>
<style scoped>
	.my-head {
		overflow: hidden;
		background: #588aff;
		color: #fff;
		font-size: 0;
		line-height: 0;
		padding-bottom: 45px;
		width: 100%;
	}

	.my-head .img1 {
		float: left;
		width: 55px;
		margin-left: 15px;
		margin-right: 15px;
		height: 55px;
		border-radius: 55px;
		box-sizing: border-box;
		border: 1px solid #fff;
		background: #fff;
	}

	.my-head .v1 {
		font-size: 15px;
		line-height: 25px;
		padding-top: 5px;
		height: 25px;
	}

	.my-head .v1 .t2 {
		font-size: 12px;
		background: #efbe3b;
		line-height: 22rpx;
		padding: 0 10rpx;
	}

	.my-head .v1 .t4 {
		font-size: 0;
		line-break: 0;
	}

	.my-head .v2 {
		float: right;
		padding: 15px 15px 0 0;
	}

	.my-head .img2 {
		width: 80px;
		height: 29px;
	}

	.listr .d1 {
		position: relative;
	}

	.listr .d1 button,
	.listr .d1 navigator {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		border: 0;
		height: 100%;
		opacity: 0;
	}

	.my-numbox {
		display: flex;
		position: relative;
		z-index: 3;
		border-radius: 5px;
		margin: -30px 15px 10px;
		height: 60px;
		background: #fff;
		box-shadow: 0 0 5px rgba(0, 0, 0, .1);
	}

	.my-numbox .nlist {
		flex: 1;
		text-align: center;
		font-size: 12px;
		color: #666;
		line-height: 16px;
	}

	.my-numbox .nlist .n {
		font-size: 20px;
		font-weight: 700;
		color: #588aff;
		line-height: 24px;
		padding: 10px 0 0;
	}

	.my-numbox .nlist .n .t1 {
		font-size: 10px;
		padding-left: 4px;
		color: #999;
		font-weight: 400;
		line-height: 14px;
	}

	button.my-getuserinfo {
		box-sizing: unset;
		padding: 0;
		text-align: left;
		background: none;
		border-radius: none;
		color: #fff;
	}

	button.my-getuserinfo::after {
		border: none;
	}

	.tj-box-h {
		height: 120px;
	}

	.tj-box {
		padding-bottom: 30px;
		position: fixed;
		width: 100%;
		left: 0;
		bottom: 0;
	}

	.tj-button {
		margin: 0 auto;
		width: 360rpx;
		height: 88rpx;
		line-height: 88rpx;
		font-size: 32rpx;
		text-align: center;
		border-radius: 50rpx;
		background: #588aff;
		color: #fff;
		box-shadow: 0 0 10px rgba(0, 0, 0, .2);
		border: 1rpx solid rgba(0, 0, 0, .1);
		animation-name: scaleDraw;
		animation-timing-function: ease-in-out;
		animation-iteration-count: infinite;
		animation-duration: 5s;
	}

	.share-bg {
		width: 100%;
		height: 100%;
		left: 0;
		top: 0;
		position: fixed;
		z-index: 9;
		background: rgba(0, 0, 0, .2);
	}

	.share-box {
		width: 100%;
		position: absolute;
		left: 0;
		bottom: 0;
		background: #fff;
	}

	.share-reset {
		text-align: center;
		font-size: 36rpx;
		border-top: 1rpx solid rgba(0, 0, 0, .1);
		height: 100rpx;
		line-height: 100rpx;
		padding-bottom: env(safe-area-inset-bottom);
	}

	.share-icon {
		display: flex;
		padding: 50rpx 20rpx 20rpx;
	}

	.share-list {
		flex: 1;
		text-align: center;
		font-size: 0;
		line-height: 0;
		position: relative;
	}

	.share-text {
		font-size: 32rpx;
		line-height: 70rpx;
		color: rgba(0, 0, 0, .6);
	}

	.share-list .img1 {
		width: 100rpx;
		height: 100rpx;
		border-radius: 10rpx;
		background-color: #999;
	}

	.share-button {
		position: absolute;
		width: 100%;
		height: 100%;
		opacity: 0;
		left: 0;
		top: 0;
	}

	@-webkit-keyframes scaleDraw {
		0% {
			transform: scale(1);
		}

		25% {
			transform: scale(1.05);
		}

		50% {
			transform: scale(1);
		}

		75% {
			transform: scale(1.05);
		}
	}

	@keyframes scaleDraw {
		0% {
			transform: scale(1);
		}

		25% {
			transform: scale(1.05);
		}

		50% {
			transform: scale(1);
		}

		75% {
			transform: scale(1.05);
		}
	}

	.coat {
		background-color: #ff1200;
		color: #fff;
		border-radius: 20px;
		height: 14px;
		line-height: 14px;
		display: inline-block;
		padding: 3px 10px;
	}

	.eventlist {
		padding-left: 5px;
		white-space: nowrap;
	}

	.eventlist,
	.eventlist .evt {
		display: inline-flex;
	}

	.eventlist .evt {
		font-size: 0;
		line-height: 0;
		padding-top: 5px;
		margin-left: 10px;
		justify-content: center;
		align-items: center;
	}

	.eventlist .evt:last-child {
		padding-right: 15px;
	}

	.eventlist .evt .img1 {
		height: 45px;
		border-radius: 5px;
		overflow: hidden;
	}

	.eventsboxscroll2 {
		width: 100%;
		font-size: 0;
		line-height: 0;
	}

	.eventlist .evt .more {
		height: 45px;
		border-radius: 5px;
		overflow: hidden;
		background-color: hsla(0, 0%, 51%, .1);
		width: 140px;
		font-size: 12px;
		text-align: center;
		color: rgba(0, 0, 0, .3);
		display: flex;
		align-items: center;
		justify-content: center;
	}
</style>
