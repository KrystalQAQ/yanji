<template>
	<view>
		<view class="booktab">
			<view catchtap="changeCloseBook" class="line{{CloseBook==0?' hover':''}}" data-data="0">使用中</view>
			<view catchtap="changeCloseBook" class="line{{CloseBook==1?' hover':''}}" data-data="1">已封账</view>
		</view>
		<view catchtap="goPage" class="booklist" data-target="blank"
			data-url="/pages/book/detail/detail?id={{item['ID']}}" wx:for="{{BookList}}" wx:key="index">
			<view class="top">
				<view class="l">
					<text class="icon_book"></text>{{item['Name']}} <text class="icon icon_vip"
						wx:if="{{item['Vip']>window.nowtime}}"></text>
				</view>
				<view class="r">{{item['CountUser']>1?item['CountUser']+'人共享账本':'1人独享账本'}}</view>
			</view>
			<view class="mid">
				<view class="ren">
					<view class="headimg" wx:if="{{userindex<10}}" wx:for="{{item.UserList}}" wx:for-index="userindex"
						wx:for-item="user">
						<image class="img1" mode="widthFix"
							src="{{user.avatarUrl!=''?user.avatarUrl:'https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/head.png'}}">
						</image>
					</view>
					<view catchtap="goPage" class="plus" data-target="blank"
						data-url="/pages/book/qrshare/qrshare?bookid={{item['ID']}}&name={{item['Name']}}"
						wx:if="{{item.CloseBook==0}}">+</view>
				</view>
			</view>
		 <view class="bot">
				<view catchtap="goPage" class="button" data-target="blank"
					data-url="/pages/book/detail/detail?id={{item['ID']}}" wx:if="{{item.CloseBook==0}}">设置</view>
				<view catchtap="goPage" class="button" data-target="blank"
					data-url="/pages/my/excel/excel?bookid={{item['ID']}}">导出</view>
				<view catchtap="goPage" class="button" data-target="blank"
					data-url="/pages/list/list?bookid={{item['ID']}}&showlist=1" wx:if="{{window.screenWidth>320}}">明细
				</view>
				<view catchtap="goPage" class="button" data-target="blank"
					data-url="/pages/list/list?bookid={{item['ID']}}">报表</view>
				<view catchtap="goPage" class="button" data-target="blank"
					data-url="/pages/book/qrshare/qrshare?bookid={{item['ID']}}&name={{item['Name']}}"
					wx:if="{{item.CloseBook==0}}">邀请</view>
				<view catchtap="goPage" class="button" data-target="top"
					data-url="/pages/index/index?nowbookid={{item['ID']}}" wx:if="{{item.CloseBook==1}}">首页查看</view>
			</view>
		</view>
		<view class="home-begin" wx:if="{{BookList==false}}">
			<image class="img1 fl" mode="widthFix" src="/images/3.png"></image>
		</view>
		<view class="height150"></view>
		<view class="add-book pd15">
			<view catchtap="joinbook" class="add-botton">加入他人账本</view>
			<view class="midd"></view>
			<view catchtap="goPage" class="add-botton" data-target="blank" data-url="/pages/book/edit/edit"
				wx:if="{{AdminBookCount==0}}">创建新的账本</view>
			<view catchtap="goSelect" class="add-botton" wx:else>创建新的账本</view>
		</view>

	</view>
</template>

<script>
</script>

<style scoped>
	.height150 {
	    height: 150px;
	}
	
	.add-book {
	    position: fixed;
	    background-color: hsla(0,0%,100%,.9);
	    box-shadow: 0 0 5px hsla(0,0%,39.2%,.1);
	    left: 0;
	    bottom: 0;
	    width: 100%;
	    box-sizing: border-box;
	    display: flex;
	    border-top: 1px solid hsla(0,0%,39.2%,.1);
	    padding-bottom: calc(15px + env(safe-area-inset-bottom));
	}
	
	.add-book .midd {
	    width: 10px;
	}
	
	.add-botton {
	    flex: 1;
	    border-radius: 24px;
	    box-shadow: 0 0 5px hsla(0,0%,39.2%,.4);
	    height: 45px;
	    line-height: 45px;
	    text-align: center;
	    color: #fff;
	    font-size: 16px;
	    background: #588aff;
	}
	
	.add-botton:first-child {
	    background-color: #ffae6c;
	}
	
	.booklist {
	    margin: 15px 15px 0;
	    background: #fff;
	    border-radius: 5px;
	    box-shadow: 0 0 15px hsla(0,0%,58.8%,.1);
	}
	
	.booklist:active {
	    background-color: hsla(0,0%,58.8%,.1);
	}
	
	.booklist .top {
	    justify-content: space-between;
	    padding: 10px 15px;
	    border-bottom: 1px solid hsla(0,0%,58.8%,.1);
	}
	
	.booklist .top,.booklist .top .l {
	    display: flex;
	    align-items: center;
	}
	
	.booklist .top .r {
	    font-size: 12px;
	    color: hsla(0,0%,39.2%,.7);
	}
	
	.booklist .top .icon_book {
	    width: 25px;
	    height: 25px;
	    margin-right: 3px;
	    background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/38.png) no-repeat 0;
	    background-size: auto 20px;
	    opacity: .8;
	}
	
	.booklist .mid {
	    border-bottom: 1px solid hsla(0,0%,58.8%,.1);
	}
	
	.booklist .bot {
	    display: flex;
	    padding: 10px 15px;
	    font-size: 12px;
	}
	
	.booklist .bot .button {
	    margin-right: 7px;
	    padding: 7px 13px;
	    color: hsla(0,0%,39.2%,.8);
	    border: 1px solid hsla(0,0%,58.8%,.2);
	    border-radius: 3px;
	}
	
	.booklist .bot .button:active {
	    background-color: hsla(0,0%,39.2%,.1);
	}
	
	.ren {
	    display: flex;
	    flex-wrap: wrap;
	    padding: 10px 15px;
	}
	
	.ren .headimg {
	    margin-right: 5px;
	    opacity: .9;
	    font-size: 0;
	    line-height: 0;
	}
	
	.ren .headimg .img1 {
	    width: 30px;
	    height: 30px;
	    border-radius: 35px;
	    overflow: hidden;
	}
	
	.plus {
	    justify-content: center;
	    width: 30px;
	    height: 30px;
	    line-height: 30px;
	    border-radius: 30px;
	    background-color: hsla(0,0%,47.1%,.1);
	}
	
	.booktab,.plus {
	    display: flex;
	    align-items: center;
	}
	
	.booktab {
	    background: hsla(0,0%,58.8%,.1);
	    border-radius: 4px;
	    box-sizing: border-box;
	    margin: 10px 15px;
	    padding: 5px;
	    text-align: center;
	    justify-items: center;
	}
	
	.booktab .line {
	    flex: 1;
	    font-size: 14px;
	    line-height: 30px;
	    height: 30px;
	    color: #646464;
	}
	
	.booktab .line.hover {
	    background-color: #fff;
	    color: #333;
	    border-radius: 4px;
	    box-sizing: border-box;
	    border: 1rpx solid hsla(0,0%,39.2%,.1);
	    box-shadow: 0 0 1rpx hsla(0,0%,39.2%,.7);
	    font-weight: 700;
	}
	
	.home-begin {
	    text-align: center;
	    padding-top: 100px;
	}
	
	.home-begin .img1 {
	    width: 150px;
	}
</style>
