<template>
	<view>
		<view class="{{BookDetail.IsVip?'vip':''}}">
		    <view class="line tline">{{UserList.length}}个共享成员</view>
		    <view class="bgfboder">
		        <view class="book-userlist">
		            <view class="list" wx:if="{{index<ShowUserCount}}" wx:for="{{UserList}}" wx:key="index">
		                <view wx:if="{{userInfo.id==BookDetail.CreateUserID}}">
		                    <image catchtap="goPage" data-target="blank" data-url="/pages/book/edit/edit_nickname?bookid={{BookDetail.ID}}&userid={{item['id']}}&nickname={{item['nickName']}}" mode="aspectFit" src="{{item['avatarUrl']==''?'https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/head.png':item['avatarUrl']}}"></image>
		                    <view catchtap="goPage" class="text" data-target="blank" data-url="/pages/book/edit/edit_nickname?bookid={{BookDetail.ID}}&userid={{item['id']}}&nickname={{item['nickName']}}">{{item['nickName']}}</view>
		                    <text bindtap="deteleUser" class="delete" data-userid="{{item['id']}}" wx:if="{{Detele==1&&userInfo.openid!=item['openid']}}">-</text>
		                    <text class="admin" wx:if="{{item['id']==BookDetail.CreateUserID}}">管理员</text>
		                </view>
		                <view wx:else>
		                    <image mode="aspectFit" src="{{item['avatarUrl']==''?'https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/head.png':item['avatarUrl']}}"></image>
		                    <view class="text">{{item['nickName']}}</view>
		                    <text catchtap="deteleUser" class="delete" data-userid="{{item['id']}}" wx:if="{{Detele==1&&userInfo.openid!=item['openid']}}">-</text>
		                    <text class="admin" wx:if="{{item['id']==BookDetail.CreateUserID}}">管理员</text>
		                </view>
		            </view>
		            <view class="list">
		                <view class="fh plus" wx:if="{{BookDetail.ShareType==0}}">+<button bindtap="shareFun" openType="share"></button>
		                </view>
		                <view class="fh plus" wx:if="{{BookDetail.ShareType==1}}">+<button bindtap="shareFunQR"></button>
		                </view>
		            </view>
		            <view bindtap="setDetele" class="list" wx:if="{{UserList.length>1&&userInfo.id==BookDetail.CreateUserID}}">
		                <view class="fh minus">-</view>
		            </view>
		        </view>
		        <view bindtap="showmoreuser" class="showmoreuser" wx:if="{{UserList.length>ShowUserCount}}">查看全部{{UserList.length}}个成员 ›</view>
		    </view>
		    <view class="line line2"></view>
		    <view class="lists bgfboder">
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/edit/edit?id={{BookDetail.ID}}&name={{BookDetail.Name}}">
		            <view class="d1">
		                <view class="d2">{{BookDetail.Name}}</view>
		      账本名称
		    </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/edit/edit_nickname?bookid={{BookDetail.ID}}&userid={{userInfo.id}}&nickname={{BookDetail.MeSet.NickName==''?userInfo.nickName:BookDetail.MeSet.NickName}}">
		            <view class="d1">
		                <view class="d2">{{BookDetail.MeSet.NickName==''?userInfo.nickName:BookDetail.MeSet.NickName}}</view>
		      我在账本的昵称
		    </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/qrshare/qrshare?bookid={{BookDetail.ID}}&name={{BookDetail.Name}}">
		            <view class="d1">
		                <view class="d2 d_icon">
		                    <text class="icon icon_qrcode"></text>
		                </view>
		                <view class="d_icon">账本二维码 <text catchtap="tip" class="icon icon_wenhao" data-tip="用于分享给朋友加入账本"></text>
		                </view>
		            </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/my/settime/settime">
		            <view class="d1">
		                <view class="d2"></view>
		                <view class="d_icon">定时提醒记账 <text catchtap="tip" class="icon icon_wenhao" data-tip="每天定时提醒自己记账"></text>
		                </view>
		            </view>
		        </view>
		        <view class="listr listrswitch">
		            <view class="d1">
		                <view class="d2">
		                    <switch bindtap="changeMeSet" checked="{{BookDetail.MeSet.PushMe==1?true:false}}" data-change="PushMe" disabled="true"></switch>
		                </view>
		                <view class="d_icon">账本变动通知 <text catchtap="tip" class="icon icon_wenhao" data-tip="账本内成员、账目发生变化通过公众号通知你"></text>
		                </view>
		            </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/auth/auth?bookid={{BookDetail.ID}}">
		            <view class="d1">
		                <view class="d2"></view>
		                <view class="d_icon">成员权限设置 <text catchtap="tip" class="icon icon_wenhao" data-tip="设定每个成员是否可以添加、修改、查看、删除账目。"></text>
		                </view>
		            </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/edit/edit_defaulttype?id={{BookDetail.ID}}&name={{BookDetail.Name}}&type={{BookDetail.DefaultType}}&transfer={{BookDetail.ShowTransfer}}">
		            <view class="d1">
		                <view class="d2">默认:{{BookDetail.DefaultType==1?'收入':'支出'}}{{BookDetail.ShowTransfer==1?',显示转账':',不显示转账'}}</view>
		                <view class="d_icon">记账默认类型 <text catchtap="tip" class="icon icon_wenhao" data-tip="添加账目页默认选中的记账类型"></text>
		                </view>
		            </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/edit/edit_display?id={{BookDetail.ID}}&name={{BookDetail.Name}}&display={{BookDetail.Display}}&startdate={{BookDetail.StartDate}}">
		            <view class="d1">
		                <view class="d2">{{BookDetail.DisplayCN}}</view>
		      首页统计方式
		    </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/edit/edit_canedit?id={{BookDetail.ID}}&name={{BookDetail.Name}}&canedit={{BookDetail.CanEdit}}">
		            <view class="d1">
		                <view class="d2">{{BookDetail.CanEdit!=null?BookDetail.CanEdit==0?'不限制':BookDetail.CanEdit+' 天后锁定':''}}</view>
		      账目锁定
		    </view>
		        </view>
		        <view class="listr listrswitch">
		            <view class="d1">
		                <view class="d2">
		                    <switch bindtap="changeMustUpImg" checked="{{BookDetail.MustUpImg==1?true:false}}" disabled="true"></switch>
		                </view>
		                <view class="d_icon">记账必须上传图片 <text catchtap="tip" class="icon icon_wenhao" data-tip="每笔账目必须上传图片"></text>
		                </view>
		            </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/examine/index?bookid={{BookDetail.ID}}">
		            <view class="d1">
		                <view class="d2"></view>
		                <view class="d_icon">成员记账审批 <text catchtap="tip" class="icon icon_wenhao" data-tip="设置账本成员记账需要他人审批入账"></text>
		                </view>
		            </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/flag/list?bookid={{BookDetail.ID}}">
		            <view class="d1">
		                <view class="d2"></view>
		                <view class="d_icon">账本预算&目标 <text catchtap="tip" class="icon icon_wenhao" data-tip="设置账本指定时间的支出和收入"></text>
		                </view>
		            </view>
		        </view>
		    </view>
		    <view class="line line2"></view>
		    <view class="lists bgfboder">
		        <view class="listr listrswitch" wx:if="{{BookDetail.FormworkID==0}}">
		            <view class="d1">
		                <view class="d2">
		                    <switch bindtap="changeShare" checked="{{BookDetail.BookType==1?true:false}}" data-change="BookType" disabled="true"></switch>
		                </view>
		                <view class="d_icon">共享账本收支条目 <text catchtap="tip" class="icon icon_wenhao" data-tip="开启后账本成员添加账目将统一成账本收支条目，关闭后账本成员将独立收支条目。"></text>
		                </view>
		            </view>
		        </view>
		        <view class="listr listrswitch" wx:else>
		            <view class="d1">
		                <view class="d2">
		                    <switch catchtap="tip" checked="{{BookDetail.BookType==1?true:false}}" data-tip="共享账本不允许关闭共享分类" disabled="true"></switch>
		                </view>
		                <view class="d_icon">共享账本收支条目 <text catchtap="tip" class="icon icon_wenhao" data-tip="开启后账本成员添加账目将统一成账本收支条目，关闭后账本成员将独立收支条目。"></text>
		                </view>
		            </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/type/type?bookid={{BookDetail.ID}}&type=1" wx:if="{{BookDetail.BookType==1}}">
		            <view class="d1">
		                <view class="d2"></view>
		                <view class="d_icon">账本收入条目</view>
		            </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/type/type?bookid={{BookDetail.ID}}&type=0" wx:if="{{BookDetail.BookType==1}}">
		            <view class="d1">
		                <view class="d2"></view>
		                <view class="d_icon">账本支出条目</view>
		            </view>
		        </view>
		        <view class="listr listrswitch" wx:if="{{BookDetail.ListCount==0}}">
		            <view class="d1">
		                <view class="d2">
		                    <switch bindtap="changeShare" checked="{{BookDetail.BookAccount==1?true:false}}" data-change="BookAccount" disabled="true"></switch>
		                </view>
		                <view class="d_icon">共享账本资金账户 <text catchtap="tip" class="icon icon_wenhao" data-tip="开启后账本成员添加账目将统一成账本资金账号，关闭后账本成员将独立资金账号。"></text>
		                </view>
		            </view>
		        </view>
		        <view class="listr listrswitch" wx:else>
		            <view class="d1">
		                <view class="d2">
		                    <switch catchtap="tip" checked="{{BookDetail.BookAccount==1?true:false}}" data-tip="该账本已经有记录账目 无法修改" disabled="true"></switch>
		                </view>
		                <view class="d_icon">共享账本资金账户 <text catchtap="tip" class="icon icon_wenhao" data-tip="开启后账本成员添加账目将统一成账本资金账号，关闭后账本成员将独立资金账号。"></text>
		                </view>
		            </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/account/account?bookid={{BookDetail.ID}}" wx:if="{{BookDetail.BookAccount==1}}">
		            <view class="d1">
		                <view class="d2"></view>
		                <view class="d_icon">账本资金账户</view>
		            </view>
		        </view>
		    </view>
		    <view class="line line2"></view>
		    <view class="lists bgfboder">
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/edit/edit_closebook?id={{BookDetail.ID}}&name={{BookDetail.Name}}&closebook={{BookDetail.CloseBook}}">
		            <view class="d1">
		                <view class="d2">{{BookDetail.CloseBook==1?'已封账':'使用中'}}</view>
		      账本状态
		    </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/list/list?bookid={{BookDetail.ID}}">
		            <view class="d1">
		                <view class="d2">{{BookDetail.ListCount?BookDetail.ListCount+'条账目':''}}</view>
		      账本统计
		    </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/search/submit?bookid={{BookDetail.ID}}">
		            <view class="d1">
		                <view class="d2"></view>
		      账单搜索
		    </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/detail/log?bookid={{BookDetail.ID}}&listid=0">
		            <view class="d1">
		                <view class="d2"></view>
		      账本日志
		    </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/img/img?bookid={{BookDetail.ID}}">
		            <view class="d1">
		                <view class="d2"></view>
		      账本图片查看
		    </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/admin/admin?bookid={{BookDetail.ID}}">
		            <view class="d1">
		                <view class="d2"></view>
		      账本管理员转移 
		    </view>
		        </view>
		    </view>
		    <view class="line line2"></view>
		    <view class="lists bgfboder">
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/vip/open?bookid={{BookDetail.ID}}" wx:if="{{version.envVersion=='release'}}">
		            <view class="d1">
		                <view class="d2">
		                    <text class="c_red" wx:if="{{BookDetail.Vip<window.nowtime}}">{{viptip}}</text>
		                    <text wx:else>已开通</text>
		                </view>
		      开通VIP账本
		    </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/my/excel/excel?bookid={{BookDetail.ID}}">
		            <view class="d1">
		                <view class="d2"></view>
		                <view class="d_icon">手动导出表格 <text class="icon icon_vip"></text>
		                </view>
		            </view>
		        </view>
		        <view bindtap="goPage" class="listr" data-target="blank" data-url="/pages/book/edit/edit_backup?bookid={{BookDetail.ID}}">
		            <view class="d1">
		                <view class="d2"></view>
		                <view class="d_icon">定期自动备份账目 <text class="icon icon_vip"></text>
		                </view>
		            </view>
		        </view>
		    </view>
		    <view class="line line2"></view>
		    <view class="pd15">
		        <button bindtap="shareFun" class="share_button" hoverClass="other-button-hover" openType="share" wx:if="{{BookDetail.ShareType==0}}">邀请伙伴加入此账本</button>
		        <button bindtap="shareFunQR" class="share_button" hoverClass="other-button-hover" wx:if="{{BookDetail.ShareType==1}}">邀请伙伴加入此账本</button>
		    </view>
		    <view class="pd15 delete_box">
		        <button bindtap="deleteBook" class="delete_button" type="warn"> 退出账本 </button>
		    </view>
		    <view class="sharebox" hidden="{{!ShareHover}}">
		        <view class="share"></view>
		    </view>
		    <view class="closebook" wx:if="{{BookDetail.CloseBook==1}}"></view>
		    <view class="height_180"></view>
		</view>

	</view>
</template>

<script>
</script>

<style scoped>
	@-webkit-keyframes warn {
	    0% {
	        transform: scale(0);
	        opacity: 0;
	    }
	
	    50% {
	        transform: scale(.5);
	        opacity: .5;
	    }
	
	    100% {
	        transform: scale(1);
	        opacity: 0;
	    }
	}
	
	@keyframes warn {
	    0% {
	        transform: scale(0);
	        opacity: 0;
	    }
	
	    50% {
	        transform: scale(.5);
	        opacity: .5;
	    }
	
	    100% {
	        transform: scale(1);
	        opacity: 0;
	    }
	}
	
	.book-userlist {
	    overflow: hidden;
	    padding-top: 10px;
	    padding-bottom: 10px;
	    padding-left: 10px;
	}
	
	.book-userlist .list {
	    width: 50px;
	    height: 70px;
	    float: left;
	    margin: 10px 10px 4px;
	    box-sizing: border-box;
	    text-align: center;
	    font-size: 12px;
	    color: #696969;
	    position: relative;
	}
	
	.book-userlist .list .text {
	    height: 18px;
	    line-height: 18px;
	    text-overflow: ellipsis;
	    overflow: hidden;
	}
	
	.book-userlist .list .fh,.book-userlist .list image {
	    font-size: 0;
	    line-height: 0;
	    width: 50px;
	    height: 50px;
	    border-radius: 5px;
	    line-height: 45px;
	}
	
	.book-userlist .list .fh {
	    box-sizing: border-box;
	    border: 1px solid #ccc;
	    position: relative;
	    color: #ccc;
	    font-size: 30px;
	}
	
	.book-userlist .list .fh button {
	    position: absolute;
	    left: 0;
	    top: 0;
	    width: 100%;
	    height: 100%;
	    opacity: 0;
	}
	
	.book-userlist .list .delete {
	    position: absolute;
	    width: 20px;
	    height: 20px;
	    background: #ff0808;
	    border-radius: 20px;
	    right: -10px;
	    z-index: 2;
	    color: #fff;
	    line-height: 20px;
	    top: -10px;
	}
	
	.book-userlist .list .admin {
	    position: absolute;
	    height: 18px;
	    background: #588aff;
	    border-radius: 18px;
	    right: -10px;
	    z-index: 2;
	    color: #fff;
	    line-height: 18px;
	    top: -7px;
	    font-size: 10px;
	    padding: 0 5px;
	    box-sizing: border-box;
	    border: 1px solid rgba(0,0,0,.1);
	}
	
	.vip .book-userlist .list .admin {
	    background-image: linear-gradient(160deg,#e4b374 20%,#daa45e 80%);
	}
	
	.sharebox {
	    position: fixed;
	    z-index: 9;
	    overflow: hidden;
	    width: 50px;
	    height: 50px;
	    top: 0;
	    right: 0;
	}
	
	.share {
	    background: #588aff;
	    width: 100px;
	    height: 100px;
	    border-radius: 50px;
	    position: absolute;
	    top: -50px;
	    left: 0;
	    animation: warn 2s linear;
	    animation-iteration-count: infinite;
	}
	
	.delete_box {
	    padding-top: 0;
	}
	
	.share_button {
	    background: #fff;
	}
	
	.delete_button,.share_button {
	    font-size: 17px;
	}
	
	@media screen and (max-width:414px) {
	    .book-userlist {
	        padding-left: 15px;
	    }
	
	    .book-userlist .list {
	        width: 53px;
	        margin: 15px 12px 2px;
	    }
	
	    .book-userlist .list image {
	        width: 53px;
	        height: 53px;
	        line-height: 53px;
	    }
	}
	
	@media screen and (max-width:375px) {
	    .book-userlist {
	        padding-left: 12px;
	    }
	
	    .book-userlist .list {
	        width: 50px;
	        margin: 10px 10px 0;
	    }
	
	    .book-userlist .list image {
	        width: 50px;
	        height: 50px;
	        line-height: 50px;
	    }
	}
	
	@media screen and (max-width:360px) {
	    .book-userlist {
	        padding-left: 10px;
	    }
	
	    .book-userlist .list {
	        width: 50px;
	        margin: 10px 9px 0;
	    }
	
	    .book-userlist .list image {
	        width: 50px;
	        height: 50px;
	        line-height: 50px;
	    }
	}
	
	@media screen and (max-width:320px) {
	    .book-userlist .list {
	        width: 54px;
	    }
	
	    .book-userlist .list image {
	        width: 54px;
	        height: 54px;
	        line-height: 54px;
	    }
	}
	
	.height_180 {
	    height: 180px;
	}
	
	.showmoreuser {
	    text-align: center;
	    font-size: 14px;
	    color: rgba(0,0,0,.6);
	    padding-top: 5px;
	    padding-bottom: 15px;
	}
	
	.closebook {
	    position: absolute;
	    top: 50px;
	    right: 30px;
	    width: 100px;
	    height: 100px;
	    background: url(https://static-1253713495.cos.ap-chengdu.myqcloud.com/jizhang/closebook.png);
	    background-size: 100px 100px;
	    z-index: 9;
	    pointer-events: none;
	    opacity: .5;
	}
</style>