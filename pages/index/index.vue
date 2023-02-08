<template>
	<view>
		<view class="home-top">
			<view class="custom_box" :style="{paddingTop:statusBarHeight+'px'}">
				<view class="custom_title" :style="{height:navBarHeight+'px'}">
					<view bindtap="changeBookBox" class="name" data-show="1">
						<!-- {{pageData.NowBook.Name}} -->默认账本
					</view>
					<view bindtap="changeBookBox" class="button" data-show="1">
						<text class="t2">切换账本</text>
					</view>
				</view>
			</view>
			<view class="home-top-v3 pdx15 {{topShow}}">
				<view bindtap="goPage" class="v vl" data-target="blank"
					data-url="/pages/book/detail/detail?id={{pageData.NowBook.ID}}">
					<image class="img1" mode="aspectFit" :src="avatarUrl"></image>
					<text wx:if="{{pageData.NowBookUserList.length>1}}">{{pageData.NowBookUserList.length}}人</text>
					<text wx:else>{{pageData.NowBookUserList.length}}人</text>
					<text class="icon_set" wx:if="{{window.windowWidth>320}}"></text>
				</view>
				<view class="v vr">
					<text bindtap="goPage" class="t4" data-target="blank"
						data-url="/pages/book/account/account?bookid={{pageData.NowBook.ID}}&noalert=1"
						wx:if="{{pageData.NowBook.BookAccount==1}}">资金</text>
					<text bindtap="goPage" class="t4" data-target="blank" data-url="/pages/my/account/account"
						wx:else>资金</text>
					<text bindtap="goPage" class="t3" data-target="blank"
						data-url="/pages/list/list?bookid={{pageData.NowBook.ID}}">报表</text>
					<text bindtap="loadPage" class="t1">
						<text class="icon_load{{textloading?' loading':''}}"></text>刷新</text>
				</view>
			</view>
			<view class="home-top-v2 pdx15">
				<view bindtap="goPage" class="v vl" data-target="blank"
					data-url="/pages/book/edit/edit_display?id={{pageData.NowBook.ID}}&name={{pageData.NowBook.Name}}&display={{pageData.NowBook.Display}}&startdate={{pageData.NowBook.StartDate}}">
					<view class="fl">
						<view class="vt">{{pageData.NowMonth}}总收入</view>
						<view class="vt" wx:if="{{pageData.AllzMoney}}">{{pageData.AllzMoney}}</view>
						<view class="vt" wx:else>0</view>
					</view>
				</view>
				<view bindtap="goPage" class="v vm" data-target="blank"
					data-url="/pages/book/edit/edit_display?id={{pageData.NowBook.ID}}&name={{pageData.NowBook.Name}}&display={{pageData.NowBook.Display}}&startdate={{pageData.NowBook.StartDate}}">
					<view class="vt">{{pageData.NowMonth}}总结余</view>
					<view class="vt" wx:if="{{pageData.AlljMoney}}">{{pageData.AlljMoney}}</view>
					<view class="vt" wx:else>0</view>
				</view>
				<view bindtap="goPage" class="v vr" data-target="blank"
					data-url="/pages/book/edit/edit_display?id={{pageData.NowBook.ID}}&name={{pageData.NowBook.Name}}&display={{pageData.NowBook.Display}}&startdate={{pageData.NowBook.StartDate}}">
					<view class="fr">
						<view class="vt">{{pageData.NowMonth}}总支出</view>
						<view class="vt" wx:if="{{pageData.AllfMoney}}">{{pageData.AllfMoney}}</view>
						<view class="vt" wx:else>0</view>
					</view>
				</view>
			</view>
		</view>
		<scroll-view bindscroll="scroll" bindscrolltolower="loadmorelist" class="scroll-view" enableBackToTop="true"
			scrollTop="{{scrollTop}}" scrollY="true" style="height:{{window.screenHeight}}px;">
			<view class="home-top-height" style="height:{{topHeight}}px;"></view>
			<view class="home-comeback" wx:if="{{pageData.Push&&pageData.Push.Tips==1&&pageData.HaveNoInsert}}">
				<swiper autoplay="true" bindtap="getfx" class="home-swiper" duration="500"
					indicatorActiveColor="rgba(0,0,0,0)" indicatorColor="rgba(0,0,0,0)" indicatorDots="false"
					interval="5000" vertical="true">
					<swiper-item wx:if="{{item.id!=pageData.userInfo.id&&item.day>0}}"
						wx:for="{{pageData.NowBookUserList}}">
						<view class="textbox">
							你的伙伴 {{item.nickName}} 已经{{item.day>100?'很久':item.day+'天'}}没有记账了。
						</view>
					</swiper-item>
				</swiper>
				<button class="home-button" openType="share">喊TA记账</button>
			</view>

			<block wx:if="{{flaglist.length>=1&&flaglist[0].ID&&flaglist[0].ID>0}}">
				<view bindtap="goPage" class="flag_list_box home" data-target="blank"
					data-url="/pages/book/flag/detail?id={{item.ID}}&bookid={{item.BookID}}&type={{item.Type}}"
					wx:for="{{flaglist}}">
					<view class="border">
						<view class="f_top">
							<view class="l">
								<text class="type type{{item.Type}}"> {{item.Type==1?'目标':'预算'}}</text> {{item.Title}}
							</view>
							<view class="r">{{item.Type==1?'达成':'完成'}}奖励：{{item.Reward==''?'未填写':item.Reward}}</view>
						</view>
						<view class="f_mid {{item.Money>10000||item.NowMoney>10000?' f_mid_small ':''}}">
							<view class="d1 l">
								<view class="percentage">
									<view class="left left{{jizhang.parseInt(item.Percentage)}}"></view>
									<view class="right right{{jizhang.parseInt(item.Percentage)}}"></view>
									<view class="progress">
										<view>
											{{item.Percentage}}%
											<view class="txt">{{item.Type==1?'达成':'剩余'}}</view>
										</view>
									</view>
								</view>
							</view>
							<view class="d1 m">
								<view>
									<view class="v1">{{item.Money}}</view>
									<view class="v2">{{item.Type==1?'目标':'预算'}}金额</view>
								</view>
							</view>
							<view class="d1 m">
								<view>
									<view class="v1">{{item.NowMoney}}</view>
									<view class="v2">{{item.Type==1?'达成':'已花费'}}金额</view>
								</view>
							</view>
							<view class="d1 r">
								<view>
									<view class="v1">{{item.AfterMoney}}</view>
									<view class="v2">{{item.Type==1?'还差':'剩余'}}金额</view>
								</view>
							</view>
						</view>
					</view>
				</view>
			</block>

			<block wx:if="{{List!=false}}" wx:for="{{List}}">
				<view class="home-list-top pdx15">
					{{item['date']}} {{item['week']}}
					收:{{item['income']}}，支:{{item['expenditure']}}，余:{{item['surplus']}}
				</view>
				<view bindlongpress="goSelect" bindtap="goDetail" class="home-list" data-id="{{item_c['ID']}}"
					data-type="{{item_c['Type']}}" wx:for="{{item.list}}" wx:for-index="index_c" wx:for-item="item_c">
					<view class="fl djbox">
						<image class="img1" mode="aspectFit" src="{{item_c['avatarUrl']}}"></image>
						<view class="icon icon_daiji"
							wx:if="{{item_c['CreateUserID']!=0&&item_c['CreateUserID']!=item_c['UserID']}}"></view>
					</view>
					<view class="d1">
						<view class="t t0 fr">
							<view class="tagbox" wx:if="{{item_c['SubType']!=0}}">
								<text class="tag" wx:if="{{item_c['SubType']==1}}">待收</text>
								<text class="tag" wx:elif="{{item_c['SubType']==2}}">待支</text>
							</view>
							<view class="moneybox">
								<block wx:if="{{item_c['Money']>0&&(item_c['Type']==1||item_c['Type']==0)}}">+</block>
								<block wx:if="{{item_c['Money']<0&&(item_c['Type']==1||item_c['Type']==0)}}">-</block>
								{{item_c['AbsMoney']}}<text class="edit img"
									wx:if="{{item_c['CanEdit']==0||item_c['Examine']==2}}"></text>
							</view>
						</view>
						<block wx:if="{{item_c['NotIncluded']==0}}">
							<text class="t t1 fl" wx:if="{{item_c['Money']<=0}}"></text>
							<text class="t t1 fl green" wx:else></text>
						</block>
						<text class="t t1 fl yellow" wx:else></text>
						<view class="t3" wx:if="{{item_c['Content']==''}}">
							<view class="t4">
								{{item_c['TypeName']}}
								<text class="icon img" wx:if="{{item_c['Img']!=''&&item_c['Img']!=null}}"></text>
								<block wx:if="{{item_c['CommentInfo']}}">
									<text class="type type{{i['Type']}}" wx:for="{{item_c['CommentInfo']}}"
										wx:for-item="i">{{i['Count']}}</text>
								</block>
							</view>
						</view>
						<view class="t3 t3t" wx:else>
							<view class="t4">
								{{item_c['TypeName']}}
								<text class="icon img" wx:if="{{item_c['Img']!=''&&item_c['Img']!=null}}"></text>
								<block wx:if="{{item_c['CommentInfo']}}">
									<text class="type type{{i['Type']}}" wx:for="{{item_c['CommentInfo']}}"
										wx:for-item="i">{{i['Count']}}</text>
								</block>
							</view>
							<view class="t5">{{item_c['Content']}}</view>
						</view>
					</view>
				</view>
			</block>
			<view bindtap="goPage" class="seemore" data-target="blank"
				data-url="/pages/list/list?showlist=1&bookid={{pageData.NowBook.ID}}"
				wx:if="{{pageData.BookAllCount>0&&pageData.List.length>100}}">这里只展示最近100条账目，<text
					class="link">查看更多></text>
			</view>
			<view class="home-bottom-height"></view>
		</scroll-view>
		<view catchtap="tapTip" class="home_fudong {{pageData.BookAllCount==0?'top':''}}"
			wx:if="{{tipShow&&pageData.TipList.length>0&&pageData.BookAllCount>0}}">
			<view class="l">
				<text catchtap="closeTip" class="icon">×</text>
				<text class="title">{{pageData.TipList[tipID].title}}</text>
			</view>
			<view class="r">
				<view class="button">{{pageData.TipList[tipID].button}}</view>
			</view>
			<button class="share-button" openType="share" wx:if="{{pageData.TipList[tipID].type=='share'}}"></button>
		</view>

		<view class="closebook" wx:if="{{pageData.NowBook.CloseBook==1}}"></view>
		<view class="menu">
			<view @click="tz('/pages/book/list/list')" class="menu-c menu-c1" data-target="blank" >
				账本
			</view>
			<view class="meun-add">
				<view @click="tz('/pages/add/add')" class="a"></view>
			</view>
			<view class="menu-c menu-c2" @click="tz('/pages/my/index/index')">
				我
			</view>
		</view>
		<view bindtap="changeJoinMy" class="join-my" style="top:{{custom.statusNavBarHeight}}px"
			wx:if="{{pageData.JoinMy==0}}">
			<image class="img1" mode="widthFix" src="/static/23{{jizhang.isios(window.system)?'':'_pc'}}.png"></image>
		</view>

		<view catchtap="changeBookBox" class="change_book_box{{changebookbox?' show':''}}" data-show="0">
			<view class="change_book">
				<view class="change_book_title">
					<text catchtap="changeBookBox" class="t1" data-show="0">取消</text>
					<text bindtap="goPage" class="t2" data-target="blank"
						data-url="/pages/book/list/list">创建或加入账本？</text>
				</view>
				<scroll-view bindrefresherrefresh="loadPage" class="change_book_scroll"
					refresherEnabled="{{!textloading}}" scrollY="true">
					<view bindtap="changeBooknew" class="list{{item.ID==pageData.NowBook.ID?' hover':''}}"
						data-bookid="{{item.ID}}" wx:for="{{pageData.BookList}}">
						<text class="l">{{item.Name}}<text class="icon icon_vip"
								wx:if="{{item.Vip>=window.nowtime}}"></text>
						</text>
						<text class="r" wx:if="{{item.ID==pageData.NowBook.ID}}">当前账本</text>
					</view>
				</scroll-view>
			</view>
		</view>
		<view class="home-nobook" wx:if="{{pageData.BookList===false}}">
			<scroll-view class="scroll" scrollY="true" style="height:{{window.windowHeight}}px;">
				<view class="bg_black_box">
					<view class="head">
						<view class="head_bg">
							<view class="main" style="width:{{window.windowWidth}}px;">
								<!-- 					<view class="logo" style="padding-top:{{custom.statusBarHeight}}px">
									<image class="img1" mode="widthFix"
										src="https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/logo.png">
									</image>
								</view> -->
								<view class="text" style="padding-top:{{custom.statusBarHeight}}px">
									{{pageData.NoBook.Title}}
								</view>
							</view>
						</view>
					</view>
					<view class="about">
						{{pageData.NoBook.Desc}}
					</view>
					<view class="nbtitle">特色功能</view>
					<view class="nbfwbzbox">
						<view class="bzbox" wx:for="{{pageData.NoBook.Fun}}">
							<view class="bzboxbg">
								<view class="icon">
									<image class="img1" mode="widthFix" src="{{item.img}}"></image>
								</view>
								<view class="t1">{{item.title}}</view>
								<view class="d1">{{item.desc}}</view>
							</view>
						</view>
					</view>
					<view class="nbtitle">服务保障</view>
					<view class="nbfwbzbox">
						<view class="bzbox">
							<view class="bzboxbg">
								<view class="icon">
									<image class="img1" mode="widthFix"
										src="https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/h1.png">
									</image>
								</view>
								<view class="t1">腾讯云服务器</view>
								<view class="d1">365天 x 24小时运行，零停机维护</view>
							</view>
						</view>
						<view class="bzbox">
							<view class="bzboxbg">
								<view class="icon">
									<image class="img1" mode="widthFix"
										src="https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/h2.png">
									</image>
								</view>
								<view class="t1">数据备份</view>
								<view class="d1">双重数据备份，云端备份，异地备份</view>
							</view>
						</view>
						<view class="bzbox">
							<view class="bzboxbg">
								<view class="icon">
									<image class="img1" mode="widthFix"
										src="https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/h3.png">
									</image>
								</view>
								<view class="t1">隐私保护</view>
								<view class="d1">从外到内严守数据关，绝不泄露信息</view>
							</view>
						</view>
						<view class="bzbox">
							<view class="bzboxbg">
								<view class="icon">
									<image class="img1" mode="widthFix"
										src="https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/h4.png">
									</image>
								</view>
								<view class="t1">技术支持</view>
								<view class="d1">7 x 12小时一对一为客户答疑解惑</view>
							</view>
						</view>
					</view>
				</view>
				<view class="add-book pd15">
					<view bindtap="joinbook" class="add-botton">加入他人账本</view>
					<view class="midd"></view>
					<view bindtap="goPageNoAuth" class="add-botton add-botton2" data-target="blank"
						data-url="/pages/book/edit/edit">创建新的账本</view>
					<view class="bt">您还没有账本，您可以选择：</view>
				</view>
			</scroll-view>
		</view>
		<!-- 		<view class="home-loading{{loadingclose?' close':''}} {{HavePassword?' password':''}}" wx:if="{{loading}}">
			<view class="logo">
				<image class="img img1" mode="widthFix" src="/static/20_1.png"></image>
				<image class="img img2" mode="widthFix" src="/static/20_2.png"></image>
				<image class="img img3" mode="widthFix" src="/static/20_3.png"></image>
			</view> -->
		<!-- 			<view id="loading-center">
				<view id="loading-center-absolute" v-if="loginfail!=true">
					<view class="object" id="object_one"></view>
					<view class="object" id="object_two" style="left:20rpx;"></view>
					<view class="object" id="object_three" style="left:40rpx;"></view>
					<view class="object" id="object_four" style="left:60rpx;"></view>
					<view class="object" id="object_five" style="left:80rpx;"></view>
				</view>
				<view bindtap="reload" class="reload" wx:else>立即登录</view>
			</view> -->
		<!-- 			<view class="home_pd_box {{HavePassword?' show':''}}">
				<view class="home_pd_title">请输入密码</view>
				<view class="home_pd_d">
					<view class="d1 {{SetPassword[0]?'ok':''}}"></view>
					<view class="d1 {{SetPassword[1]?'ok':''}}"></view>
					<view class="d1 {{SetPassword[2]?'ok':''}}"></view>
					<view class="d1 {{SetPassword[3]?'ok':''}}"></view>
				</view>
				<view class="home_pd_list">
					<view class="home_pd_line">
						<view bindtap="setpassword" class="button" data-number="1">1</view>
					</view>
					<view class="home_pd_line">
						<view bindtap="setpassword" class="button" data-number="2">2</view>
					</view>
					<view class="home_pd_line">
						<view bindtap="setpassword" class="button" data-number="3">3</view>
					</view>
					<view class="home_pd_line">
						<view bindtap="setpassword" class="button" data-number="4">4</view>
					</view>
					<view class="home_pd_line">
						<view bindtap="setpassword" class="button" data-number="5">5</view>
					</view>
					<view class="home_pd_line">
						<view bindtap="setpassword" class="button" data-number="6">6</view>
					</view>
					<view class="home_pd_line">
						<view bindtap="setpassword" class="button" data-number="7">7</view>
					</view>
					<view class="home_pd_line">
						<view bindtap="setpassword" class="button" data-number="8">8</view>
					</view>
					<view class="home_pd_line">
						<view bindtap="setpassword" class="button" data-number="9">9</view>
					</view>
					<view class="home_pd_line">
						<view bindtap="setpassword" class="button" data-number="?">?</view>
					</view>
					<view class="home_pd_line">
						<view bindtap="setpassword" class="button" data-number="0">0</view>
					</view>
					<view class="home_pd_line">
						<view bindtap="setpassword" class="button" data-number="x">x</view>
					</view>
				</view>
			</view>
			<view class="slogan">免费 / 稳定 / 安全 / 强大 / 便捷</view>
		</view> -->

	</view>
</template>

<script>
	export default {
		data() {
			return {
				avatarUrl: "",
				statusBarHeight: "",
				navBarHeight: "",
				custom: {},
				loginfail: !1,
				userInfo: {},
				changebookbox: !1,
				GetUserInfo: 1,
				HavePassword: !1,
				SetPassword: [],
				BookForID: 0,
				NowBookID: 0,
				Inviter: 0,


				topShow: "",
				textloading: !0,
				zhangTitle: "共享记账",
				loading: !0,
				loadingclose: !1,
				tipShow: !1,
				tipID: -1,
				zhibo: {},
				flaglist: [],
				List: [],
				page: 1,
				scrollTop: 0,
				Loadmore: 1,
				pageData: {
					NowMonth: Number(new Date().getMonth()) + 1 + "月",
					AllzMoney: 0,
					AllfMoney: 0,
					BookAllCount: 0,
					MyAllCount: -1,
					AdShow: 0,
					JoinMy: 1
				},
				changeBookList: null
			}
		},
		onLoad() {

			try {
				const value = uni.getStorageSync('mp_wx_openid');
				var mp_wx_openid = JSON.parse(value).mp_wx_openid
				if (JSON.parse(value).mp_wx_openid) {
					this.avatarUrl = JSON.parse(value).avatarUrl
					console.log(mp_wx_openid);
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
			this.GetStatusBarHeight();
		},
		methods: {
			tz(e) {
			// console.log("hello")
				uni.navigateTo({
					url: e,
				});

			},
			GetStatusBarHeight() {
				let that = this;
				wx.getSystemInfo({
					success: function(res) {
						that.statusBarHeight = res.statusBarHeight;

						const demo = uni.getMenuButtonBoundingClientRect()
						var l = demo.top
						console.log("top", l)
						console.log("height", demo.height)
						that.navBarHeight = demo.height + 2 * (l - res.statusBarHeight)
						console.log("that.navBarHeight", that.navBarHeight)

					},
				});
			},
		}
	}
</script>

<style scoped>
	.home-top {
		position: fixed;
		background: #588aff;
		left: 0;
		top: 0;
		width: 100%;
		box-sizing: border-box;
		z-index: 9;
	}

	.home-top-v1 {
		height: 45px;
		line-height: 45px;
		color: #fff;
		display: flex;
	}

	.home-top-v1.none {
		display: none;
	}

	.home-top-v1 .v {
		flex: 1;
	}

	.home-top-v1 .vm {
		text-align: center;
		font-size: 17px;
		font-weight: 500;
	}

	.home-top-v1 .vl {
		text-align: left;
		height: 45px;
		position: relative;
	}

	.home-top-v1 .vl image {
		float: left;
	}

	.home-top-v1 .vl .img1 {
		width: 28px;
		height: 28px;
		border-radius: 28px;
		border: 1px solid #fff;
		box-sizing: border-box;
		margin-top: 8px;
	}

	.home-top-v1 .vl .img2 {
		width: 20px;
		height: 20px;
		border-radius: 20px;
		border: 1rpx solid #fff;
		box-sizing: border-box;
		margin-top: 8px;
		margin-left: -10px;
	}

	.home-top-v1 .vl text {
		font-size: 15px;
		font-weight: 300;
		display: inline-block;
		padding: 2px 4px;
		background: #3398ff;
		border: 1rpx solid #fff;
		border-radius: 10px;
		font-size: 7px;
		height: 7px;
		line-height: 7px;
		position: absolute;
		top: 10px;
		left: 15px;
	}

	.home-top-v1 .vr {
		text-align: right;
		font-size: 15px;
		font-weight: 300;
	}

	.home-top-v1 .vr .t1 {
		display: inline-block;
		background: url(https://i1.piimg.com/533270/a0175d30cbbc1e02.png) no-repeat 0;
		background-size: 15px 15px;
		padding-left: 20px;
	}

	.home-top-v2 {
		height: 60px;
		color: #fff;
		display: flex;
		font-size: 14px;
		text-align: center;
		line-height: 20px;
	}

	.home-top-v2 .v {
		flex: 1;
		padding-top: 10px;
	}

	.home-top-v2 .fl {
		float: left;
	}

	.home-top-v2 .fr {
		float: right;
	}

	.home-top-v3 {
		height: 24px;
		margin-bottom: 4px;
		margin-top: 7px;
	}

	.home-top-v3 .vl {
		float: left;
	}

	.home-top-v3 .vl .img1 {
		width: 24px;
		height: 24px;
		margin-right: 2px;
	}

	.home-top-v3 .vl .img1,
	.home-top-v3 .vl text {
		border: 1rpx solid #fff;
		border-radius: 12px;
		box-sizing: border-box;
		float: left;
	}

	.home-top-v3 .vl text {
		color: #fff;
		font-size: 12px;
		height: 20px;
		line-height: 20px;
		padding: 0 10px;
		margin-top: 2px;
		margin-left: 1px;
		font-weight: 300;
	}

	.home-top-v3 .vl text.icon_set {
		border: none;
		border-radius: 0;
		background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/36.png) no-repeat 50%;
		background-size: 18px 18px;
		margin-left: 4px;
	}

	.home-top-v3 .vr {
		float: right;
		line-height: 24px;
		text-align: right;
		font-size: 15px;
		font-weight: 400;
		color: #fff;
	}

	.home-top-v3 .vr .t1 {
		display: inline-block;
	}

	.home-top-v3 .vr .t1 .icon_load {
		display: inline-block;
		background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/4.png) no-repeat 0;
		background-size: 18px 18px;
		width: 18px;
		height: 18px;
		margin-right: 4px;
		position: relative;
		top: 3px;
	}

	.home-top-v3 .vr .t1 .icon_load.loading {
		animation: turn 1s linear infinite;
	}

	.home-top-v3 .vr .t1:active {
		color: hsla(0, 0%, 100%, .5);
	}

	@-webkit-keyframes turn {
		0% {
			-webkit-transform: rotate(0deg);
		}

		25% {
			-webkit-transform: rotate(90deg);
		}

		50% {
			-webkit-transform: rotate(180deg);
		}

		75% {
			-webkit-transform: rotate(270deg);
		}

		100% {
			-webkit-transform: rotate(1turn);
		}
	}

	@keyframes turn {
		0% {
			-webkit-transform: rotate(0deg);
		}

		25% {
			-webkit-transform: rotate(90deg);
		}

		50% {
			-webkit-transform: rotate(180deg);
		}

		75% {
			-webkit-transform: rotate(270deg);
		}

		100% {
			-webkit-transform: rotate(1turn);
		}
	}

	.custom_title .button .t2 {
		margin-left: 10px;
		font-size: 14px;
		opacity: .7;
	}

	.custom_title .button .t2,
	.home-top-v3 .vr .t2 {
		display: inline-block;
		background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/5.png) no-repeat 0;
		background-size: 18px 18px;
		padding-left: 22px;
		margin-right: 15px;
	}

	.home-top-v3 .vr .t3 {
		background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/37.png) no-repeat 0;
		background-size: 18px 18px;
	}

	.home-top-v3 .vr .t3,
	.home-top-v3 .vr .t4 {
		display: inline-block;
		padding-left: 22px;
		margin-right: 15px;
	}

	.home-top-v3 .vr .t4 {
		background: url(https://static-1253713495.file.myqcloud.com/jizhang/card.png) no-repeat 0;
		background-size: 18px 18px;
	}

	.home-top-v3 .vr .picker {
		display: inline-block;
	}

	.home-top-v3.none {
		display: none;
	}

	.home-bottom-height {
		height: 200px;
	}

	.home-list-top {
		background: #f8f8f8;
		font-size: 10px;
		color: #a2a2a2;
		height: 22px;
		line-height: 22px;
		position: sticky;
		top: 60px;
		z-index: 2;
	}

	.home-list-topbox {
		height: 22px;
	}

	.home-list {
		background: #fff;
		box-sizing: border-box;
		width: 100%;
		padding-left: 15px;
		height: 55px;
		overflow: hidden;
	}

	.home-list .djbox {
		position: relative;
	}

	.home-list .djbox .icon_daiji {
		left: 5px;
		top: 37px;
		position: absolute;
		width: 20px;
		height: 9px;
		background-size: 100% 100%;
		opacity: 1;
	}

	.home-list .img1 {
		width: 30px;
		height: 30px;
		background: #fff;
		box-sizing: border-box;
		border-radius: 30px;
		border: 1rpx solid #bababa;
		margin-top: 14px;
		float: left;
	}

	.home-list .d1 {
		box-sizing: border-box;
		height: 55px;
		border-bottom: 1rpx solid #eee;
		margin-left: 45px;
	}

	.home-list .d1 .t0 {
		float: right;
		height: 55px;
		color: #474747;
		font-size: 15px;
		padding-right: 15px;
		display: flex;
		align-items: flex-end;
		justify-content: center;
		flex-direction: column;
		line-height: 20px;
	}

	.home-list .d1 .t0 .tag {
		font-size: 10px;
		background-color: #fff;
		line-height: 14px;
		color: #588aff;
		border: 1rpx solid #588aff;
		opacity: .8;
		border-radius: 4px;
		padding: 0 4px;
	}

	.home-list .d1 .t0.green {
		color: #04c030;
	}

	.home-list .d1 .t0.red {
		color: #fa2121;
	}

	.home-list .d1 .t0 .edit {
		width: 16px;
		height: 16px;
		display: inline-block;
		margin-left: 8px;
		vertical-align: middle;
		background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/30.png) no-repeat top;
		background-size: 16px auto;
		opacity: .2;
	}

	.home-list .d1 .t1 {
		float: left;
		width: 8px;
		height: 8px;
		border-radius: 8px;
		background: #ff1200;
		margin-top: 24px;
		margin-right: 8px;
	}

	.home-list .d1 .t1.green {
		background: #04c030;
	}

	.home-list .d1 .t1.yellow {
		background: #f88a39;
	}

	.home-list .d1 .t3 {
		color: #474747;
		font-size: 15px;
		line-height: 55px;
	}

	.home-list .d1 .t3 .t4 .icon {
		width: 16px;
		height: 16px;
		display: inline-block;
		margin-left: 8px;
		vertical-align: middle;
	}

	.home-list .d1 .t3 .t4 .icon.img {
		background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/27.png) no-repeat 50%;
		background-size: 16px auto;
	}

	.home-list .d1 .t3 .t4 .type {
		height: 16px;
		line-height: 16px;
		display: inline-block;
		margin-left: 8px;
		vertical-align: middle;
		color: #6d9afa;
		font-size: 10px;
		padding: 0 0 0 19px;
	}

	.home-list .d1 .t3 .t4 .type1 {
		background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/27_pl.png) no-repeat 0;
		background-size: 16px auto;
	}

	.home-list .d1 .t3 .t4 .type2 {
		background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/27_pl2.png) no-repeat 0;
		color: #ffa133;
		background-size: 16px auto;
	}

	.home-list .d1 .t3 .t4 .type3 {
		background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/27_pl3.png) no-repeat 0;
		color: #fa2121;
		background-size: 16px auto;
	}

	.home-list .d1 .t3 .t4 .type4 {
		background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/27_pl4.png) no-repeat 0;
		background-size: 16px auto;
	}

	.home-list .d1 .t3t {
		line-height: 18px;
	}

	.home-list .d1 .t3t .t4 {
		padding-top: 11px;
	}

	.home-list .d1 .t3t .t5 {
		font-size: 12px;
		color: #949494;
		height: 18px;
		overflow: hidden;
		margin-right: 120px;
		text-overflow: ellipsis;
	}

	.home-list:active {
		background-color: #eee;
	}

	.scroll-view {
		background: #f8f8f8;
	}

	.home-begin {
		text-align: center;
		padding-top: 100px;
	}

	.home-begin .img1 {
		width: 150px;
	}

	.home-frist {
		position: fixed;
		left: 50%;
		margin-left: -6px;
		bottom: calc(70px + constant(safe-area-inset-bottom));
		bottom: calc(70px + env(safe-area-inset-bottom));
		z-index: 2;
	}

	.home-frist .img1 {
		width: 100px;
	}

	.home-frist-yaoqing {
		position: fixed;
		left: 20px;
		top: 135px;
		z-index: 9;
	}

	.home-frist-yaoqing .img1 {
		width: 150px;
	}

	.ad-box {
		position: fixed;
		top: 0;
		left: 0;
		font-size: 0;
		line-height: 0;
		width: 100%;
		height: 100%;
		z-index: 10;
		background: rgba(0, 0, 0, .5);
		text-align: center;
	}

	.ad-box .imgbox {
		width: 260px;
		margin: 0 auto 20px;
		padding-top: 15%;
	}

	.ad-box .button-box,
	.ad-box .imgbox image {
		width: 100%;
	}

	.ad-box .ad-button {
		box-sizing: unset;
		margin: 0;
		padding: 0 20px;
		background: none;
		border-radius: 50px;
		height: 35px;
		line-height: 35px;
		display: inline-block;
		border: 3px solid #fff;
		color: #fff;
		font-size: 14px;
		font-weight: 700;
	}

	.home-comeback {
		position: relative;
		background: #ffec82;
		border-bottom: 1px solid #e2e2e2;
		height: 40px;
	}

	.home-comeback .home-swiper {
		height: 40px;
	}

	.home-comeback .textbox {
		color: #6f6f6f;
		font-size: 12px;
		line-height: 40px;
		padding-left: 15px;
	}

	.home-comeback .home-button {
		text-shadow: 1px 1px 0 rgba(0, 0, 0, .2);
		box-shadow: 0 0 3px rgba(0, 0, 0, .3);
		box-sizing: content-box;
		position: absolute;
		font-size: 14px;
		border-radius: 50px;
		right: 12px;
		padding: 0 10px;
		height: 24px;
		line-height: 24px;
		top: 7px;
		color: #fff;
		background: #f88a39;
		border: 1px solid rgba(0, 0, 0, .1);
	}

	.home-comeback .home-button::after {
		border: none;
		width: auto;
	}

	.home-loading {
		position: fixed;
		z-index: 998;
		width: 100%;
		height: 100%;
		background: #588aff;
		top: 0;
		left: 0;
		transition: all 1s;
	}

	.home-loading.close {
		left: -800rpx;
	}

	.home-loading .slogan {
		position: absolute;
		text-align: center;
		left: 0;
		bottom: 0;
		width: 100%;
		color: #fff;
		font-size: 24rpx;
		line-height: 36rpx;
		padding-bottom: 30rpx;
	}

	.home-loading .logo {
		width: 100%;
		position: relative;
	}

	.home-loading .logo image {
		width: 100%;
		top: 40px;
		position: absolute;
		left: 0;
	}

	.home-loading.password .logo image {
		transition: all 1s;
	}

	.home-loading.password .logo .img1 {
		opacity: .3;
	}

	.home-loading.password .logo .img2 {
		top: -60px;
	}

	.home-loading.password .logo .img3 {
		opacity: 0;
	}

	.home-loading.password #loading-center {
		display: none;
	}

	.home_pd_box {
		-o-transition: all 1s;
		-webkit-transition: all 1s;
		opacity: 0;
		text-align: center;
		position: absolute;
		width: 100%;
		bottom: 0;
		left: 0;
		color: #fff;
		padding-bottom: 100px;
	}

	.home_pd_box.show {
		opacity: 1;
	}

	.home_pd_d {
		font-size: 0;
		line-height: 0;
		padding: 30px 0;
	}

	.home_pd_d .d1 {
		margin: 0 5px;
		display: inline-block;
		width: 10px;
		height: 10px;
		border-radius: 10px;
		border: 1px solid hsla(0, 0%, 100%, .5);
	}

	.home_pd_d .d1.ok {
		background-color: #fff;
	}

	.home_pd_list {
		display: flex;
		flex-wrap: wrap;
		padding: 0 50px;
	}

	.home_pd_list .home_pd_line {
		padding: 8px 0;
		width: 33.333%;
	}

	.home_pd_list .home_pd_line,
	.home_pd_list .home_pd_line .button {
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.home_pd_list .home_pd_line .button {
		width: 65px;
		height: 65px;
		border-radius: 65px;
		border: 1px solid hsla(0, 0%, 100%, .8);
		font-size: 18px;
	}

	.home_pd_list .home_pd_line .button:active {
		background-color: hsla(0, 0%, 100%, .5);
	}

	.home_pd_list .home_pd_line:nth-child(10),
	.home_pd_list .home_pd_line:nth-child(12) {
		opacity: .5;
	}

	.seemore {
		text-align: center;
		font-size: 12px;
		padding-top: 30px;
	}

	.seemore .link {
		color: #4169e1;
		border-bottom: 1px solid #4169e1;
	}

	.home-nobook {
		position: fixed;
		top: 0;
		left: 0;
		height: 100%;
		width: 100%;
		background-color: #000;
		z-index: 997;
	}

	.home-nobook .scroll {
		height: 100%;
		width: 100%;
		position: relative;
	}

	.home-nobook .head {
		text-align: center;
		color: #fff;
		position: relative;
		height: 350px;
	}

	.home-nobook .head .head_bg {
		position: absolute;
		width: 180%;
		background-color: #588aff;
		border-bottom-left-radius: 150%;
		border-bottom-right-radius: 150%;
		top: 0;
		left: 50%;
		margin-left: -90%;
		overflow: hidden;
	}

	.home-nobook .head .head_bg .main {
		position: relative;
		margin: 0 auto;
		height: 350px;
		background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/jizhang_guanwang/top-phone.png) no-repeat center 110px;
		background-size: 100% auto;
	}

	.home-nobook .head .head_bg .main .text {
		position: absolute;
		top: 55px;
		text-align: center;
		width: 100%;
		font-size: 22px;
	}

	.home-nobook .head .head_bg .logo {
		position: absolute;
		left: 15px;
		top: 0;
		height: 45px;
		display: flex;
		align-items: center;
	}

	.home-nobook .head .head_bg .logo .img1 {
		width: 80px;
	}

	.home-nobook .about {
		font-size: 14px;
		padding: 30px 20px;
		color: rgba(0, 0, 0, .5);
		text-align: center;
		line-height: 22px;
	}

	.home-nobook .bg_black {
		display: flex;
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(0, 0, 0, .2);
	}

	.home-nobook .bg_black_box {
		background-color: #fff;
		opacity: .8;
	}

	.home-nobook .nbtitle {
		text-align: center;
		font-size: 22px;
		color: rgba(0, 0, 0, .8);
	}

	.nbfwbzbox {
		display: flex;
		flex-wrap: wrap;
		padding: 10px 15px 40px;
	}

	.nbfwbzbox .bzbox {
		box-sizing: border-box;
		width: 50%;
		padding: 10px;
	}

	.nbfwbzbox .bzbox .bzboxbg {
		box-shadow: 0 0 12px hsla(0, 0%, 58.8%, .2);
		padding: 15px;
		border-radius: 10px;
		text-align: center;
	}

	.nbfwbzbox .bzbox .bzboxbg .icon {
		font-size: 0;
		line-height: 0;
	}

	.nbfwbzbox .bzbox .bzboxbg .icon .img1 {
		width: 30px;
		height: 30px;
	}

	.nbfwbzbox .bzbox .bzboxbg .t1 {
		padding-bottom: 10px;
		padding-top: 5px;
	}

	.nbfwbzbox .bzbox .bzboxbg .d1 {
		font-size: 12px;
		line-height: 18px;
		height: 36px;
		overflow: hidden;
		color: rgba(0, 0, 0, .5);
	}

	.nbfwbzbox:last-child {
		padding-bottom: 200px;
	}

	.home-nobook .add-book {
		position: fixed;
		background-color: #fff;
		box-shadow: 0 0 5px hsla(0, 0%, 39.2%, .1);
		left: 0;
		bottom: 0;
		width: 100%;
		box-sizing: border-box;
		display: flex;
		border-top: 1px solid hsla(0, 0%, 39.2%, .1);
		padding-top: 50px;
		padding-bottom: calc(25px + env(safe-area-inset-bottom));
	}

	.home-nobook .add-book .midd {
		width: 10px;
	}

	.home-nobook .add-botton {
		flex: 1;
		border-radius: 24px;
		box-shadow: 0 0 5px hsla(0, 0%, 39.2%, .4);
		height: 45px;
		line-height: 45px;
		text-align: center;
		color: #fff;
		font-size: 16px;
		background: #588aff;
	}

	.home-nobook .add-botton2 {
		animation-name: bulePulse;
		animation-duration: 2s;
		animation-iteration-count: infinite;
	}

	.home-nobook .add-botton:first-child {
		background-color: #ffae6c;
	}

	.closebook {
		position: fixed;
		top: 200px;
		right: 30px;
		width: 100px;
		height: 100px;
		background: url(https://static-1253713495.cos.ap-chengdu.myqcloud.com/jizhang/closebook.png);
		background-size: 100px 100px;
		z-index: 9;
		pointer-events: none;
		opacity: .8;
	}

	@-webkit-keyframes bulePulse {
		from {
			box-shadow: 0 0 5px hsla(0, 0%, 39.2%, .4);
		}

		50% {
			box-shadow: 0 0 27px #588aff;
		}

		to {
			box-shadow: 0 0 5px hsla(0, 0%, 39.2%, .4);
		}
	}

	@keyframes bulePulse {
		from {
			box-shadow: 0 0 5px hsla(0, 0%, 39.2%, .4);
		}

		50% {
			box-shadow: 0 0 27px #588aff;
		}

		to {
			box-shadow: 0 0 5px hsla(0, 0%, 39.2%, .4);
		}
	}

	.home-nobook .add-book .bt {
		position: absolute;
		top: 15px;
		left: 0;
		text-align: center;
		width: 100%;
		font-size: 14px;
		color: rgba(0, 0, 0, .4);
	}

	#loading-center {
		position: relative;
		left: 0;
		top: 0;
		z-index: 3;
		height: 100%;
	}

	#loading-center-absolute {
		position: absolute;
		left: 50%;
		top: 70%;
		height: 20rpx;
		width: 100rpx;
		margin-top: -10rpx;
		margin-left: -50rpx;
	}

	.home-loading .reload {
		position: absolute;
		left: 50%;
		top: 70%;
		color: hsla(0, 0%, 100%, .9);
		border-radius: 100px;
		border: 1px solid hsla(0, 0%, 100%, .5);
		width: 130px;
		text-align: center;
		font-size: 14px;
		line-height: 40px;
		margin-left: -65px;
		margin-top: -20px;
	}

	.home-loading .reload:active {
		background-color: hsla(0, 0%, 100%, .1);
	}

	.join-my {
		position: fixed;
		top: 0;
		right: 40rpx;
		z-index: 10;
		animation: heart 1.3s ease-in-out 2.7s 6 alternate;
	}

	.join-my .img1 {
		width: 318rpx;
	}

	.home_fudong {
		z-index: 2;
		display: flex;
		justify-content: space-between;
		color: hsla(0, 0%, 100%, .9);
		box-sizing: border-box;
		padding: 4px 15px;
		position: fixed;
		bottom: calc(80px + constant(safe-area-inset-bottom));
		bottom: calc(80px + env(safe-area-inset-bottom));
		width: 300px;
		left: 50%;
		margin-left: -150px;
		border-radius: 100px;
		background-color: rgba(0, 0, 0, .6);
		font-size: 12px;
		line-height: 24px;
	}

	.home_fudong .icon {
		display: inline-block;
		background-color: hsla(0, 0%, 100%, .5);
		color: #000;
		width: 20px;
		height: 20px;
		line-height: 20px;
		text-align: center;
		border-radius: 60px;
		margin-left: -5px;
		margin-right: 10px;
	}

	.home_fudong .button {
		color: #f88a39;
	}

	.home_fudong .share-button {
		position: absolute;
		top: 0;
		right: 0;
		border-radius: 0;
		background-color: hsla(0, 0%, 100%, 0);
		width: 260px;
		border: none;
		height: 32px;
	}

	.home_fudong.top {
		bottom: calc(150px + constant(safe-area-inset-bottom));
		bottom: calc(150px + env(safe-area-inset-bottom));
	}

	.object {
		width: 15rpx;
		height: 15rpx;
		background-color: #fff;
		border-radius: 50% 50% 50% 50%;
		margin-right: 20rpx;
		margin-bottom: 20rpx;
		position: absolute;
	}

	#object_one {
		animation: object 2s linear infinite;
	}

	#object_two {
		animation: object 2s linear -.4s infinite;
	}

	#object_three {
		animation: object 2s linear -.8s infinite;
	}

	#object_four {
		animation: object 2s linear -1.2s infinite;
	}

	#object_five {
		animation: object 2s linear -1.6s infinite;
	}

	@-webkit-keyframes object {
		0% {
			left: 100rpx;
			top: 0;
		}

		80% {
			left: 0;
			top: 0;
		}

		85% {
			left: 0;
			top: -20rpx;
			width: 15rpx;
			height: 15rpx;
		}

		90% {
			width: 25rpx;
			height: 8rpx;
		}

		95% {
			left: 100rpx;
			top: -20rpx;
			width: 15rpx;
			height: 15rpx;
		}

		100% {
			left: 100rpx;
			top: 0;
		}
	}

	@keyframes object {
		0% {
			left: 100rpx;
			top: 0;
		}

		80% {
			left: 0;
			top: 0;
		}

		85% {
			left: 0;
			top: -20rpx;
			width: 15rpx;
			height: 15rpx;
		}

		90% {
			width: 25rpx;
			height: 8rpx;
		}

		95% {
			left: 100rpx;
			top: -20rpx;
			width: 15rpx;
			height: 15rpx;
		}

		100% {
			left: 100rpx;
			top: 0;
		}
	}

	@-webkit-keyframes heart {
		from {
			transform: translate(0, 0);
		}

		to {
			transform: translate(0, 12rpx);
		}
	}

	@keyframes heart {
		from {
			transform: translate(0, 0);
		}

		to {
			transform: translate(0, 12rpx);
		}
	}

	.search_icon .main {
		padding: 7px 10px;
		box-sizing: border-box;
		width: 100%;
		background: #fff;
	}

	.search_icon .main .v1 {
		color: hsla(0, 0%, 39.2%, .7);
		background: hsla(0, 0%, 39.2%, .1);
		border-radius: 90px;
		height: 30px;
		line-height: 30px;
		text-align: center;
		font-size: 14px;
		display: flex;
		align-items: center;
		justify-content: flex-start;
		padding-left: 15px;
	}

	.search_icon .main .t1 {
		width: 16px;
		height: 16px;
		display: inline-block;
		background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/39.png) no-repeat 50%;
		background-size: 16px 16px;
		margin-right: 5px;
		opacity: .3;
	}

	.search_icon .main .search_examine {
		color: #666;
	}

	.search_icon .main .search_examine .col {
		color: #f88a39;
	}

	.flag_list_box.home {
		margin-right: 10px;
		margin-left: 10px;
		margin-bottom: 5px;
	}

	.flag_list_box.home .border {
		box-shadow: 0 0 5rpx hsla(0, 0%, 39.2%, .3);
		color: rgba(0, 0, 0, .5);
		background-color: #fff;
		background-image: linear-gradient(180deg, #fff 20%, #f5f5f5 80%);
	}

	.flag_list_box.home .f_top {
		color: rgba(0, 0, 0, .5);
	}

	.flag_list_box.home .f_mid .d1.l {
		width: 120rpx;
		flex: none;
		padding-left: 30rpx;
		padding-right: 30rpx;
	}

	.flag_list_box.home .f_mid .d1 .v1 {
		color: #588aff;
		font-size: 40rpx;
		line-height: 45rpx;
	}

	.flag_list_box.home .f_mid .d1 .v2 {
		color: rgba(0, 0, 0, .5);
	}

	.flag_list_box.home .progress {
		background-color: #fff;
		color: #f88a39;
	}

	.flag_list_box.home .f_mid {
		padding-bottom: 25rpx;
		padding-right: 40rpx;
		flex-wrap: wrap;
	}

	.flag_list_box.home .f_mid_small .d1 .v1 {
		color: #588aff;
		font-size: 30rpx;
		line-height: 35rpx;
	}

	.flag_list_box.home .percentage {
		transform: scale(1);
	}

	.openvideo {
		margin-top: 20%;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.openvideo .icon {
		width: 22px;
		height: 22px;
		margin-right: 5px;
	}
</style>
