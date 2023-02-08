<template>
	<view>
		<form bindsubmit="submit" reportSubmit="true">
		    <view class="body" style="min-height:{{window.windowHeight}}px;">
		        <view id="add_head">
		            <view class="pd15 bgf add-type">
		                <view class="add-d1">
		                    <block wx:for="{{ParentTypeList}}" wx:key="index">
		                        <view catchtap="changeParentSubTypeID" class="add-d1-li hover" data-id="{{item['ID']}}" wx:if="{{pageData.ParentTypeID==item['ID']}}">
		                            <block wx:if="{{pageData.SubType==0}}">{{item['Name']}}</block>
		                            <block wx:elif="{{pageData.SubType==1}}">待收</block>
		                            <block wx:elif="{{pageData.SubType==2}}">待支</block>
		                            <block wx:elif="{{pageData.SubType==3}}">借出</block>
		                            <block wx:elif="{{pageData.SubType==4}}">借入</block>
		                            <text class="delta"></text>
		                        </view>
		                        <view catchtap="changeParentTypeID" class="add-d1-li" data-id="{{item['ID']}}" wx:else>
		              {{item['Name']}}
		            </view>
		                    </block>
		                    <view bindtap="goPage" class="add-d1-li" data-new="1" data-target="self" data-url="/pages/add/transfer?bookid={{NowBook.ID}}" wx:if="{{NowBook.ShowTransfer==1}}">
		              内部转账
		          </view>
		                </view>
		            </view>
		            <view class="pd15 add-line" wx:if="{{window.screenHeight<700}}">请输入金额</view>
		            <view class="bgf add-input add-input1" wx:if="{{window.screenHeight<700}}">
		                <input bindinput="changeMoney" confirmType="done" placeholder="0.00" type="digit" value="{{pageData.Money}}"></input>
		            </view>
		            <view bindtap="showkeyboard" class="bgf add-input add-input1" wx:if="{{window.screenHeight>=700}}">
		                <view class="new_money {{pageData.Money==''?'zero':''}}">{{pageData.Money==''?'0.00':pageData.Money}}</view>
		            </view>
		        </view>
		        <block wx:if="{{pageData.SubType!=3&&pageData.SubType!=4}}">
		            <view class="pd15 add-line">请选择分类</view>
		            <view class="bgf add-select">
		                <scroll-view class="scroll" id="type_scroll" scrollLeft="{{scrollLeft}}" scrollX="true">
		                    <block wx:if="{{item['Type']==pageData.ParentTypeID}}" wx:for="{{TypeList}}" wx:key="ID">
		                        <text class="add-select-text hover" data-id="{{item['ID']}}" wx:if="{{pageData.TypeID==item['ID']||pageData.TypeID==0&&index==0}}">{{item['Name']}}</text>
		                        <text catchtap="changeTypeID" class="add-select-text" data-id="{{item['ID']}}" wx:else>{{item['Name']}}</text>
		                    </block>
		                    <text bindtap="goPage" class="add-select-text add-type-style" data-new="1" data-target="blank" data-url="/pages/my/plus/plus?type={{pageData.ParentTypeID}}" wx:if="{{NowBook.BookType!=1}}">+</text>
		                    <text bindtap="goPage" class="add-select-text add-type-style" data-new="1" data-target="blank" data-url="/pages/book/type/type?type={{pageData.ParentTypeID}}&bookid={{NowBook.ID}}" wx:else>+</text>
		                </scroll-view>
		                <view bindtap="changeTypeListIsShow" class="more">
		                    <text class="icon"></text>
		                </view>
		            </view>
		        </block>
		        <block wx:if="{{pageData.SubType!=1&&pageData.SubType!=2}}">
		            <view class="pd15 add-line">请选择账户</view>
		            <view class="bgf add-select">
		                <scroll-view class="scroll" scrollX="true">
		                    <block wx:for="{{AccountList}}" wx:key="index">
		                        <text class="add-select-text hover" data-id="{{item['ID']}}" wx:if="{{pageData.AccountID==item['ID']||pageData.AccountID==0&&index==0}}">{{item['Name']}}</text>
		                        <text catchtap="changeAccountID" class="add-select-text" data-id="{{item['ID']}}" wx:else>{{item['Name']}}</text>
		                    </block>
		                    <text bindtap="goPage" class="add-select-text add-type-style" data-new="1" data-target="blank" data-url="/pages/my/account/account" wx:if="{{NowBook.BookAccount!=1}}">+</text>
		                    <text bindtap="goPage" class="add-select-text add-type-style" data-new="1" data-target="blank" data-url="/pages/book/account/account?bookid={{NowBook.ID}}" wx:else>+</text>
		                </scroll-view>
		            </view>
		        </block>
		        <view class="pd15 add-line">备注</view>
		        <view class="add-img-box">
		            <view class="pd15 bgf add-textarea">
		                <textarea bindblur="bindTextAreaBlur" bindfocus="focusContent" bindinput="changeContent" value="{{pageData.Content}}"></textarea>
		            </view>
		            <view bindtap="selectimg" class="upload-box" wx:if="{{pageData.Img==''}}">
		                <view class="imgbox">
		                    <image class="img1" mode="widthFix" src="/static/26.png"></image>
		                </view>
		                <view class="upload-text">上传图片</view>
		            </view>
		            <view class="upload-img-box" wx:else>
		                <view bindtap="deleteimg" class="close1">×</view>
		                <image bindtap="goShowImg" class="img1" mode="aspectFit" src="{{pageData.Img}}"></image>
		            </view>
		        </view>
		        <block wx:if="{{pageData.Location!=false&&pageData.Location!=''}}">
		            <view class="pd15 add-line">位置信息</view>
		            <view catchtap="getLoaction" class="bgf add-location-info">
		                <view class="name">{{pageData.Location.name}}</view>
		                <view class="address">{{pageData.Location.address}}</view>
		                <view catchtap="closeLoaction" class="close">×</view>
		            </view>
		        </block>
		        <view class="datenew">
		            <view class="datenew_left">
		                <view bindtap="getLoaction" class="add-loaction" wx:if="{{pageData.Location==false||pageData.Location==''}}"></view>
		                <view bindtap="formatCreateDate2" class="add-time2">
		                    <image class="img1" mode="widthFix" src="/static/29.png"></image>
		            {{showCreateDate}}
		        </view>
		            </view>
		            <view bindtap="showUserBox" class="select_user" wx:if="{{pageData.UserInfo&&pageData.UserInfo.id&&pageData.UserInfo.id!=0}}">
		                <view>{{pageData.ParentTypeID==1?'收入':'支出'}}人</view>
		                <view class="add_head">
		                    <image class="img1" mode="widthFix" src="{{pageData.UserInfo.avatarUrl}}"></image>
		                    <text class="name">{{pageData.UserInfo.nickName}}</text>
		                </view>
		            </view>
		        </view>
		        <view class="pd15 add-submit-box" wx:if="{{window.screenHeight<700}}">
		            <button class="add-submit" formType="submit">完成</button>
		        </view>
		        <view class="keyboard {{KeyboardDou?'dou':''}}" wx:if="{{window.screenHeight>=700}}">
		            <view class="left">
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="button" data-number="7">7</button>
		                </view>
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="button" data-number="8">8</button>
		                </view>
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="button" data-number="9">9</button>
		                </view>
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="button" data-number="4">4</button>
		                </view>
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="button" data-number="5">5</button>
		                </view>
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="button" data-number="6">6</button>
		                </view>
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="button" data-number="1">1</button>
		                </view>
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="button" data-number="2">2</button>
		                </view>
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="button" data-number="3">3</button>
		                </view>
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="button" data-number=".">.</button>
		                </view>
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="button" data-number="0">0</button>
		                </view>
		                <view class="buttonbox">
		                    <button catchlongtap="pushKey" catchtap="pushKey" class="button" data-number="C">
		                        <text class="icon icon_huishan"></text>
		                    </button>
		                </view>
		            </view>
		            <view class="right">
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="button" data-number="-">-</button>
		                </view>
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="button" data-number="+">+</button>
		                </view>
		                <view class="buttonbox">
		                    <button catchtap="pushKey" class="plus button" data-number="=" wx:if="{{HavePlus==1}}">=</button>
		                    <button class="submit button" formType="submit" wx:else>保存</button>
		                </view>
		            </view>
		        </view>
		        <view class="more_typelist" style="height:{{typeHeight}}px;top:{{typeTop}}px;" wx:if="{{typeListIsShow}}">
		            <scroll-view scrollY="true" style="height:{{typeHeight}}px;">
		                <view class="more_typelist_box">
		                    <view catchtap="changeTypeID" class="add-select-text" data-id="{{item['ID']}}" wx:if="{{item['Type']==pageData.ParentTypeID}}" wx:for="{{TypeList}}" wx:key="ID">{{item['Name']}}</view>
		                </view>
		            </scroll-view>
		            <view class="setting">
		                <switch bindchange="changeTypeDefault" checked="{{defaultOpenType}}" class="wx_switch_input" color="#588aff" type="switch"></switch>默认展开
		      </view>
		        </view>
		    </view>
		</form>
		<view class="gang_box" wx:if="{{Addok}}">
		    <image class="img1" mode="widthFix" src="https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/gang.png"></image>
		    <view class="bai">
		        <block wx:if="{{MyAll.Count}}">
		            <view class="p1">已记账</view>
		            <view class="p2">
		                <text class="t1">{{MyAll.Day}}<text class="t2">天</text>
		                </text>
		            </view>
		            <view class="p3">{{MyAll.Text}}</view>
		            <view class="p4">
		          已记录
		          <text class="t1">{{MyAll.Count}}</text>
		          笔账目
		        </view>
		        </block>
		        <block wx:else>
		            <view class="addok_tip">{{AddokInfo.tip}}</view>
		            <view catchtap="tapTip" class="addok_main" wx:if="{{AddokInfo.Ad}}">
		                <image class="img3" mode="widthFix" src="{{AddokInfo.Ad.img}}" wx:if="{{AddokInfo.Ad.img!=''}}"></image>
		                <view class="text">
		                    <view class="title" wx:if="{{AddokInfo.Ad.title!=''}}">{{AddokInfo.Ad.title}}</view>
		                    <view class="button" wx:if="{{AddokInfo.Ad.button!=''}}">{{AddokInfo.Ad.button}}</view> 
		                </view>
		            </view>
		        </block>
		        <view catchtap="goHome" class="colse">×</view>
		        <view class="buttonbox">
		            <view class="share">
		                <button bindtap="shareShow" class="share-button" openType="share">给TA看账</button>
		            </view>
		            <view class="oncemore" wx:if="{{pageData.ID==0}}">
		                <button bindtap="oncemore" class="oncemore-button">再记一笔</button>
		            </view>
		        </view>
		    </view>
		</view>
		<view class="change_book_box {{ShowUserListBox?' show':''}}">
		    <view class="change_book">
		        <view class="change_book_title">
		            <text class="t1">请选择{{pageData.ParentTypeID==1?'收入':'支出'}}人：</text>
		            <text bindtap="showUserListBox" class="t2">完成</text>
		        </view>
		        <scroll-view class="scroll" scrollY="{{true}}">
		            <view class="lists bgfboder">
		                <radio-group bindchange="changeUserID" class="radioChange">
		                    <label class="label" wx:for="{{AddOthers.BookUserList}}" wx:key="{{item.id}}">
		                        <view class="listr adminuser">
		                            <view class="d1">
		                                <view class="d2">
		                                    <radio checked="{{item.id==pageData.UserInfo.id?true:false}}" value="{{item.id}}"></radio>
		                                </view>
		                                <view class="d5">
		                                    <image class="headimg" mode="widthFix" src="{{item.avatarUrl}}"></image>
		                            {{item.nickName}}
		                        </view>
		                            </view>
		                        </view>
		                    </label>
		                </radio-group>
		            </view>
		        </scroll-view>
		    </view>
		</view>
		<view class="canvasbox">
		    <canvas canvasId="canvas1" class="canvas1" id="canvas1"></canvas>
		</view>
		<calendar bind:close="calendarClose" bind:getdate="cmfClick" class="calendar" id="calendar" isOpen="{{true}}" multiple="{{false}}" selected="{{[pageData.CreateDate]}}" wx:if="{{calendarOpen}}"></calendar>

	</view>
</template>

<script>
</script>

<style scoped>
	.add-type {
	    padding-top: 15px;
	    padding-bottom: 15px;
	}
	
	.add-d1 {
	    height: 30px;
	    border: 1rpx solid #588aff;
	    border-radius: 4px;
	    overflow: hidden;
	}
	
	.add-d1,.add-d1-li {
	    box-sizing: border-box;
	    display: flex;
	}
	
	.add-d1-li {
	    flex: 1;
	    text-align: center;
	    line-height: 30px;
	    font-size: 15px;
	    color: #588aff;
	    align-items: center;
	    justify-content: center;
	}
	
	.add-d1-li.hover {
	    background: #588aff;
	    color: #fff;
	}
	
	.add-d1-li:nth-child(2) {
	    border-left: 1rpx solid #588aff;
	    border-right: 1rpx solid #588aff;
	}
	
	.add-line {
	    border-bottom: 1rpx solid #ebebeb;
	    border-top: 1rpx solid #ebebeb;
	    padding-top: 0;
	    padding-bottom: 0;
	    line-height: 25px;
	    height: 25px;
	    font-size: 12px;
	    color: #b5b5b5;
	    font-weight: 300;
	}
	
	.add-input1 {
	    position: relative;
	    padding-left: 15px;
	}
	
	.add-input1 input {
	    line-height: 60px;
	    height: 60px;
	    font-size: 40px;
	    font-weight: 300;
	    color: #4a4a4a;
	}
	
	.money_type {
	    position: absolute;
	    right: 15px;
	    top: 13px;
	    font-size: 12px;
	    border: 1rpx solid rgba(0,0,0,.3);
	    line-height: 24px;
	    height: 24px;
	    display: inline-block;
	    padding: 0 10px;
	    color: rgba(0,0,0,.3);
	    border-radius: 20px;
	    background-color: #fff;
	}
	
	.add-submit-box {
	    position: fixed;
	    left: 0;
	    bottom: 0;
	    width: 100%;
	    z-index: 7;
	}
	
	.add-submit {
	    border-radius: 24px;
	    height: 48px;
	    line-height: 48px;
	    text-align: center;
	    color: #fff;
	    font-size: 20px;
	    background: #588aff;
	}
	
	.add-submit:active {
	    opacity: .8;
	}
	
	.add-select {
	    position: relative;
	}
	
	.add-select .more {
	    position: absolute;
	    top: 0;
	    right: 0;
	    height: 100%;
	    width: 30px;
	    display: flex;
	    padding-right: 10px;
	    justify-content: flex-end;
	    align-items: center;
	    background-image: linear-gradient(90deg,hsla(0,0%,100%,0) 20%,#fff 80%);
	    color: #ccc;
	}
	
	.add-select .more .icon {
	    width: 16px;
	    height: 16px;
	    display: block;
	    background-image: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/7.png);
	    background-repeat: no-repeat;
	    background-size: auto 100%;
	    transform: rotate(90deg);
	    margin-top: 10px;
	    opacity: .5;
	}
	
	.add-select .scroll {
	    padding: 10px 0;
	    width: 100%;
	    box-sizing: border-box;
	    height: 54px;
	    white-space: nowrap;
	    overflow: hidden;
	    text-overflow: ellipsis;
	}
	
	.add-select-y .scroll {
	    padding: 10px 0 10px 15px;
	    width: 100%;
	    box-sizing: border-box;
	    white-space: normal;
	    height: auto;
	}
	
	.add-select-text {
	    box-sizing: border-box;
	    font-size: 14px;
	    border: 1rpx solid #588aff;
	    line-height: 34px;
	    height: 34px;
	    display: inline-block;
	    padding: 0 19px;
	    color: #588aff;
	    border-radius: 20px;
	    margin-right: 10px;
	}
	
	.add-select-text.hover {
	    background: #588aff;
	    color: #fff;
	}
	
	.add-select .scroll .add-select-text:nth-child(1) {
	    margin-left: 15px;
	}
	
	.add-select .scroll .add-select-text:last-child {
	    margin-right: 45px;
	}
	
	.add-select-y .scroll .add-select-text {
	    margin-bottom: 10px;
	}
	
	.add-select-y .scroll .add-select-text:nth-child(1) {
	    margin-left: 0;
	}
	
	.add-type-style {
	    border-color: rgba(0,0,0,.1);
	    color: rgba(0,0,0,.2);
	    font-size: 20px;
	    vertical-align: top;
	    padding: 0 15px;
	}
	
	.add-time {
	    padding-top: 0;
	    padding-bottom: 0;
	    color: #4a4a4a;
	    font-size: 14px;
	    height: 45px;
	    line-height: 45px;
	    position: relative;
	}
	
	.add-textarea {
	    border-bottom: 1rpx solid #ebebeb;
	    padding-top: 10px;
	    padding-bottom: 10px;
	    margin-right: 71px;
	}
	
	.add-textarea textarea {
	    font-size: 14px;
	    color: #4a4a4a;
	    width: 100%;
	    line-height: 28px;
	    height: 50px;
	}
	
	.add-img-box {
	    position: relative;
	}
	
	.datenew_left {
	    display: flex;
	    align-items: center;
	}
	
	.add-loaction {
	    width: 20px;
	    height: 20px;
	    background: url("https://static-1253713495.file.myqcloud.com/jizhang/location.png") no-repeat 50%;
	    background-size: auto 100%;
	    margin-right: 10px;
	}
	
	.add-location-info {
	    position: relative;
	    background: url("https://static-1253713495.file.myqcloud.com/jizhang/location.png") no-repeat 15px #fff;
	    background-size: 20px auto;
	    padding: 10px 0 10px 40px;
	}
	
	.add-location-info .name {
	    font-size: 14px;
	}
	
	.add-location-info .address {
	    font-size: 12px;
	    line-height: 16px;
	    color: rgba(0,0,0,.3);
	    height: 16px;
	    overflow: hidden;
	}
	
	.add-location-info .close {
	    position: absolute;
	    font-size: 16px;
	    width: 24px;
	    height: 24px;
	    border-radius: 24px;
	    background-color: #fff;
	    border: 1px solid rgba(0,0,0,.1);
	    display: flex;
	    align-items: center;
	    justify-content: center;
	    right: 15px;
	    top: 15px;
	}
	
	.upload-box {
	    position: absolute;
	    right: 0;
	    top: 0;
	    font-size: 12px;
	    width: 71px;
	    height: 71px;
	    background: #588aff;
	    text-align: center;
	    color: #fff;
	}
	
	.upload-box .img1 {
	    width: 25px;
	}
	
	.upload-box .imgbox {
	    padding-top: 15px;
	}
	
	.upload-img-box {
	    overflow: hidden;
	    position: absolute;
	    right: 0;
	    top: 0;
	    font-size: 12px;
	    width: 71px;
	    height: 71px;
	    background: #a5a5a5;
	    text-align: center;
	    color: #fff;
	}
	
	.upload-img-box .img1 {
	    width: 71px;
	    height: 71px;
	    opacity: .8;
	}
	
	.upload-img-box .close1 {
	    position: absolute;
	    width: 20px;
	    height: 20px;
	    line-height: 20px;
	    background: hsla(0,0%,100%,.8);
	    color: rgba(0,0,0,.5);
	    font-size: 16px;
	    top: 5px;
	    right: 5px;
	    border-radius: 20px;
	    z-index: 2;
	}
	
	.add-time-today {
	    position: absolute;
	    right: 10px;
	    top: 9px;
	    height: 27px;
	    color: #588aff;
	    line-height: 27px;
	    text-align: center;
	    font-size: 12px;
	    border: 1rpx solid #588aff;
	    padding: 0 10px;
	    border-radius: 20px;
	}
	
	.add-time-today:active {
	    background: #588aff;
	    color: #fff;
	}
	
	.gang_box {
	    display: flex;
	    flex-flow: column;
	    display: -webkit-box;
	    display: -moz-box;
	    -webkit-box-pack: center;
	    -moz-box-pack: center;
	    -webkit-box-align: center;
	    -moz-box-align: center;
	    position: fixed;
	    background: rgba(50,50,50,.1);
	    top: 0;
	    left: 0;
	    width: 100%;
	    height: 100%;
	    z-index: 10;
	    overflow: hidden;
	    box-sizing: border-box;
	    padding: 30px;
	}
	
	.gang_box .img1 {
	    -webkit-animation: circle 50s linear infinite;
	    top: 50%;
	    opacity: .5;
	    margin-top: -400px;
	    width: 800px;
	    height: 800px;
	    position: absolute;
	    left: 50%;
	    margin-left: -400px;
	}
	
	.gang_box .bai {
	    position: relative;
	    z-index: 2;
	    min-height: 150px;
	    width: 100%;
	    max-width: 330px;
	    background: #fff;
	    border-radius: 20px;
	    box-sizing: border-box;
	    box-shadow: 0 0 15px rgba(0,0,0,.1);
	    margin-top: -100px;
	}
	
	.gang_box .bai .p1 {
	    text-align: center;
	    color: #e56611;
	    font-size: 16px;
	    padding-top: 20px;
	    line-height: 30px;
	    height: 30px;
	}
	
	.gang_box .bai .p2 {
	    text-align: center;
	    color: #e56611;
	    height: 70px;
	    letter-spacing: -2px;
	}
	
	.gang_box .bai .p2 .t1 {
	    font-size: 70px;
	    line-height: 70px;
	    position: relative;
	}
	
	.gang_box .bai .p2 .t2 {
	    font-size: 14px;
	    position: absolute;
	    right: -20px;
	    bottom: 20px;
	    line-height: 16px;
	}
	
	.gang_box .bai .p3 {
	    padding: 3px 10px;
	    font-size: 12px;
	    line-height: 14px;
	    border-radius: 20px;
	    background: #f3f3f3;
	    text-align: center;
	    color: #a5a5a5;
	    margin: 15px 15px 0;
	}
	
	.gang_box .bai .p4 {
	    text-align: center;
	    font-weight: 100;
	    font-size: 14px;
	    color: #949494;
	    padding-top: 20px;
	    padding-bottom: 20px;
	}
	
	.gang_box .bai .p4 .t1 {
	    color: #e56611;
	    font-weight: 700;
	}
	
	.gang_box .bai .colse {
	    font-size: 16px;
	    position: absolute;
	    top: -8px;
	    right: -7px;
	    background: #e7e7e7;
	    border-radius: 30px;
	    border: 8px solid #fff;
	    color: #fff;
	    text-align: center;
	    line-height: 30px;
	    width: 30px;
	}
	
	.gang_box .bai .addok_tip {
	    border-bottom: 1rpx solid rgba(0,0,0,.1);
	    text-align: center;
	    font-size: 20px;
	    font-weight: 700;
	    padding: 30px 0 25px;
	    color: rgba(0,0,0,.7);
	}
	
	.gang_box .bai .addok_main {
	    margin-bottom: 30px;
	    padding: 20px 20px 0;
	}
	
	.gang_box .bai .addok_main .img3 {
	    width: 100%;
	}
	
	.gang_box .bai .addok_main .text {
	    display: flex;
	    align-items: center;
	    flex-wrap: wrap;
	    font-size: 14px;
	    color: #b0b0b0;
	}
	
	.gang_box .bai .addok_main .text .title {
	    flex: 1;
	    box-sizing: border-box;
	    padding-right: 10px;
	}
	
	.gang_box .bai .addok_main .text .button {
	    border: 1rpx solid #b0b0b0;
	    border-radius: 20px;
	    padding: 3px 15px;
	}
	
	.buttonbox {
	    display: flex;
	    padding-top: 15px;
	    padding-bottom: 30px;
	    margin: 0 auto;
	    max-width: 250px;
	}
	
	.gang_box .share {
	    flex: 1;
	}
	
	.gang_box .share .share-button {
	    margin: 0 auto;
	    width: 110px;
	    height: 40px;
	    line-height: 40px;
	    font-size: 14px;
	    text-align: center;
	    border-radius: 25px;
	    background: #588aff;
	    color: #fff;
	    box-shadow: 0 0 10px rgba(0,0,0,.2);
	    border: 1rpx solid rgba(0,0,0,.1);
	    animation-name: scaleDraw;
	    animation-timing-function: ease-in-out;
	    animation-iteration-count: infinite;
	    animation-duration: 5s;
	}
	
	.gang_box .oncemore {
	    flex: 1;
	}
	
	.gang_box .oncemore .oncemore-button {
	    margin: 0 auto;
	    width: 110px;
	    height: 40px;
	    line-height: 40px;
	    font-size: 14px;
	    text-align: center;
	    border-radius: 25px;
	    background: #f88a39;
	    color: #fff;
	    box-shadow: 0 0 10px rgba(0,0,0,.2);
	    border: 1rpx solid rgba(0,0,0,.1);
	}
	
	.gang_box .oncemore .oncemore-button:active {
	    opacity: .8;
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
	
	@-webkit-keyframes circle {
	    0% {
	        transform: rotate(0deg);
	    }
	
	    100% {
	        transform: rotate(-1turn);
	    }
	}
	
	.datenew {
	    padding: 10px 12px 10px 15px;
	    font-size: 12px;
	    display: flex;
	    justify-content: space-between;
	}
	
	.datenew .img1 {
	    width: 20px;
	    margin-right: 5px;
	    opacity: .7;
	}
	
	.datenew .add-time2 {
	    color: rgba(0,0,0,.7);
	}
	
	.datenew .add-time2,.datenew .select_date {
	    display: flex;
	    align-items: center;
	}
	
	.datenew .select_date {
	    width: 150px;
	}
	
	.datenew .select_user {
	    flex-wrap: wrap;
	    color: rgba(0,0,0,.7);
	}
	
	.datenew .select_user,.datenew .select_user .add_head {
	    display: flex;
	    align-items: center;
	}
	
	.datenew .select_user .add_head {
	    background-color: rgba(0,0,0,.1);
	    height: 26px;
	    padding: 0 8px 0 5px;
	    border-radius: 90px;
	    margin-left: 5px;
	    box-sizing: border-box;
	    border: 1rpx solid #fff;
	}
	
	.datenew .select_user .add_head .img1 {
	    border-radius: 20px;
	}
	
	.keyboard {
	    position: fixed;
	    bottom: 0;
	    left: 0;
	    width: 100%;
	    padding-bottom: calc(2px + env(safe-area-inset-bottom));
	    flex-wrap: nowrap;
	    z-index: 9;
	    background-color: #fff;
	    box-shadow: 0 0 10px hsla(0,0%,39.2%,.1);
	    -o-transition: bottom .2s;
	    -webkit-transition: bottom .2s;
	}
	
	.keyboard,.keyboard .left {
	    display: flex;
	}
	
	.keyboard .left {
	    flex: 1;
	    flex-wrap: wrap;
	}
	
	.keyboard .right {
	    width: 90px;
	}
	
	.keyboard .left .buttonbox {
	    width: 33.33333%;
	    box-sizing: border-box;
	    padding: 1rpx 1rpx 1rpx 0;
	}
	
	.keyboard .right .buttonbox {
	    box-sizing: border-box;
	    padding: 1rpx;
	}
	
	.keyboard .buttonbox .button {
	    font-weight: 700;
	    font-size: 18px;
	    height: 55px;
	    line-height: 55px;
	    background-image: linear-gradient(to top right,#f9f9f9,#ededed);
	    border: 0;
	    border-radius: 0;
	    width: 100%;
	    display: flex;
	    justify-content: center;
	    align-items: center;
	}
	
	.keyboard .buttonbox .button::after {
	    border: none;
	}
	
	.keyboard .right .buttonbox .button {
	    height: 55px;
	    line-height: 55px;
	}
	
	.keyboard .right .buttonbox:last-child .button {
	    height: 111px;
	    line-height: 111px;
	}
	
	.keyboard .right .buttonbox:last-child .button.submit {
	    background-image: linear-gradient(to top right,#6098ff,#588aff);
	    color: #fff;
	}
	
	.keyboard .right .buttonbox:last-child .button.plus {
	    background-image: linear-gradient(to top right,#fda21a,#fda21a);
	    color: #fff;
	}
	
	.keyboard .buttonbox .button:active {
	    background: rgba(0,0,0,.1);
	}
	
	.new_money {
	    font-size: 36px;
	    line-height: 50px;
	    padding-bottom: 5px;
	}
	
	.new_money.zero {
	    color: rgba(0,0,0,.5);
	}
	
	.keyboard.dou {
	    bottom: -10px;
	}
	
	.canvasbox {
	    position: relative;
	    overflow: hidden;
	    width: 0;
	    height: 0;
	    z-index: -99;
	}
	
	.canvas1 {
	    width: 640px;
	    height: 9000px;
	    position: absolute;
	    top: -2000px;
	    left: -2000px;
	}
	
	.change_book_box .change_book .change_book_title {
	    margin-bottom: 10px;
	}
	
	.change_book_box .change_book .change_book_title .t2 {
	    color: #588aff;
	}
	
	.change_book_box .bgfboder {
	    border-top: none;
	    border-bottom: none;
	}
	
	.change_book_box .lists .radioChange .listr {
	    padding: 0;
	}
	
	.change_book_box .lists .radioChange .listr .d2 {
	    background: none;
	    padding-right: 0;
	    margin-right: 0;
	}
	
	.change_book_box .lists .radioChange .listr .d1 {
	    height: 45px;
	    line-height: 45px;
	    box-sizing: border-box;
	    border-bottom: 1rpx solid #eee;
	    font-size: 15px;
	    color: #333;
	}
	
	.change_book_box .lists .radioChange .label:last-child .listr .d1 {
	    border-bottom: none;
	}
	
	.change_book_box .headimg {
	    width: 25px;
	    height: 25px;
	    border-radius: 25px;
	    margin-right: 10px;
	}
	
	.change_book_box .adminuser .d5 {
	    display: flex;
	    align-items: center;
	}
	
	.change_book_box .scroll {
	    max-height: 400px;
	}
	
	.more_typelist_box {
	    padding: 15px 0 60px 15px;
	}
	
	.more_typelist {
	    background: #fff;
	    top: 118px;
	    z-index: 8;
	    padding-bottom: calc(0px + env(safe-area-inset-bottom));
	}
	
	.more_typelist,.more_typelist .setting {
	    position: absolute;
	    box-sizing: border-box;
	    width: 100%;
	}
	
	.more_typelist .setting {
	    bottom: 0;
	    left: 0;
	    font-size: 12px;
	    padding: 10px 15px;
	    text-align: right;
	    display: flex;
	    justify-content: flex-end;
	    align-items: center;
	    color: #b0b0b0;
	    background-color: #fff;
	}
	
	.more_typelist .add-select-text {
	    margin-right: 8px;
	    margin-bottom: 8px;
	}
	
	.wx_switch_input {
	    zoom: .7;
	    margin-right: 5px;
	}
	
	.calendar {
	    position: fixed;
	    bottom: 0;
	    left: 0;
	    width: 100%;
	    z-index: 9;
	}
	
	.delta {
	    display: inline-block;
	    font-size: 0;
	    line-height: 0;
	    width: 0;
	    height: 0;
	    border-color: #fff transparent transparent;
	    border-style: solid;
	    border-width: 5px 5px 0;
	    margin-left: 3px;
	}
</style>