<template>
	
	<view>
		<view class="line tline">账本名称</view>
		<view class="bgfboder">
		    <input bindinput="changeName" class="bgfinput" focus="{{Focus}}" maxlength="18" placeholder="请输入账本名称" value="{{Name}}"></input>
		</view>
		<view class="line" wx:if="{{CopyBookList==0&&TypeIndex!=-1}}">账本类型</view>
		<view class="lists bgfboder" wx:if="{{CopyBookList==0&&TypeIndex!=-1}}">
		    <label bindtap="showBookType">
		        <view class="listr">
		            <view class="d1">
		                <view class="iconl">
		                    <image class="icon" mode="widthFix" src="{{TypeList[TypeIndex].Img}}"></image>
		                  {{TypeList[TypeIndex].Name}}
		                </view>
		                <view class="d2">
		                    <radio checked="true" value="1"></radio>
		                </view>
		            </view>
		        </view>
		    </label>
		</view>

		<view class="pd15">
		    <button bindtap="submit" type="primary">确 定</button>
		</view>

	</view>
</template>

<script>
</script>

<style scoped>
	.lists .listr .d2 {
	    background: none;
	    padding-right: 0;
	    height: 55px;
	    line-height: 55px;
	}
	
	.lists .listr .d1 {
	    height: 55px;
	    line-height: 55px;
	    box-sizing: border-box;
	    border-bottom: 1rpx solid #eee;
	    font-size: 15px;
	    color: #333;
	    justify-content: space-between;
	}
	
	.lists .listr .d1,.lists .listr .d1 .iconl {
	    display: flex;
	    align-items: center;
	}
	
	.lists .listr .d1 .icon {
	    width: 25px;
	    height: 25px;
	    border-radius: 25px;
	    margin-right: 10px;
	}
	
	.lists .listr .d1 .icon_book {
	    width: 25px;
	    height: 25px;
	    background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/38.png) no-repeat 0;
	    background-size: auto 20px;
	    opacity: .8;
	}
	
	.booktypelist {
	    padding: 15px;
	    box-sizing: border-box;
	    position: fixed;
	    background-color: #f8f8f8;
	    width: 100%;
	    height: 100%;
	    left: 0;
	    top: 0;
	    z-index: 2;
	}
	
	.typelist {
	    box-shadow: 0 0 15px hsla(0,0%,58.8%,.1);
	    background-color: #fff;
	    border-radius: 5px;
	    overflow: hidden;
	    margin-top: 15px;
	}
	
	.typelist .label {
	    display: flex;
	    justify-content: space-between;
	    padding: 13px 10px 13px 15px;
	}
	
	.typelist .label .img {
	    display: flex;
	    align-items: center;
	    justify-content: center;
	}
	
	.typelist .label .img1 {
	    width: 40px;
	    height: 40px;
	    border-radius: 30px;
	}
	
	.typelist .label .left {
	    display: flex;
	    align-items: center;
	}
	
	.typelist .label .text {
	    padding-left: 10px;
	}
	
	.typelist .label .right {
	    display: flex;
	    align-items: center;
	}
	
	.typelist .label .info {
	    font-size: 12px;
	    color: #969696;
	}
	
	.typelist .label .icon_book {
	    width: 25px;
	    height: 25px;
	    background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/38.png) no-repeat 0;
	    background-size: auto 20px;
	    opacity: .8;
	}
	
	.lists .checkboxChange .listr .d2 {
	    background: none;
	    padding-right: 0;
	    height: 45px;
	    line-height: 45px;
	}
	
	.lists .checkboxChange .listr .d1 {
	    height: 45px;
	    line-height: 45px;
	    box-sizing: border-box;
	    border-bottom: 1rpx solid #eee;
	    font-size: 15px;
	    color: #333;
	    display: block;
	}
</style>