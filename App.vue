<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	
	input,page {
	    font-family: PingFang SC,Lantinghei SC,Helvetica Neue,Helvetica,Arial,Microsoft YaHei,微软雅黑,STHeitiSC-Light,simsun,宋体,WenQuanYi Zen Hei,WenQuanYi Micro Hei,"sans-serif";
	}
	
	.bgf {
	    background: #fff;
	}
	
	.pd15 {
	    padding: 15px;
	}
	
	.pd15,.pd20 {
	    box-sizing: border-box;
	}
	
	.pd20 {
	    padding: 20px;
	}
	
	.pdx15 {
	    padding: 0 15px;
	    box-sizing: border-box;
	}
	
	.c_red {
	    color: tomato;
	}
	
	.menu {
	    position: fixed;
	    z-index: 9;
	    left: 0;
	    bottom: 0;
	    width: 100%;
	    box-sizing: border-box;
	    height: calc(50px + constant(safe-area-inset-bottom));
	    height: calc(50px + env(safe-area-inset-bottom));
	    background: #fcfcfc;
	    border-top: 1rpx solid #e8e8e8;
	    display: flex;
	    padding-bottom: env(safe-area-inset-bottom);
	    box-shadow: 0 0 10px rgba(0,0,0,.1);
	}
	
	.menu-c {
	    flex: 1;
	    text-align: center;
	    font-size: 10px;
	    color: #8d8d8d;
	    background-size: 23px 23px;
	    background-position: center 5px;
	    padding-top: 33px;
	    line-height: 11px;
	    background-repeat: no-repeat;
	}
	
	.menu-c1 {
	    background-image: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/app1.png);
	}
	
	.menu-c2 {
	    background-image: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/app2.png);
	}
	
	.menu-c3 {
	    background-image: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/app3.png);
	}
	
	.menu-c1.hover {
	    color: #588aff;
	    background-image: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/app4.png);
	}
	
	.menu-c2.hover {
	    color: #588aff;
	    background-image: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/app5.png);
	}
	
	.meun-add {
	    width: 68px;
	    height: 49px;
	    margin: 0 auto;
	    position: relative;
	}
	
	.meun-add .a {
	    width: 68px;
	    height: 68px;
	    background: #588aff url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/app6.png) no-repeat 50%;
	    background-size: 30px 30px;
	    border-radius: 68px;
	    position: absolute;
	    left: 0;
	    bottom: -5px;
	    box-shadow: 0 0 10px rgba(0,0,0,.1);
	}
	
	.meun-add .a:active {
	    background-color: #73a8ff;
	}
	
	.bgfboder {
	    background: #fff;
	    border-bottom: 1rpx solid #ebebeb;
	    border-top: 1rpx solid #ebebeb;
	}
	
	.bgfinput {
	    height: 45px;
	    lighting-color: 45px;
	    font-size: 16px;
	    padding: 0 15px;
	}
	
	.line {
	    padding-left: 15px;
	    padding-right: 15px;
	    line-height: 25px;
	    height: 25px;
	    font-size: 12px;
	    color: #b5b5b5;
	    font-weight: 300;
	}
	
	.line.tline {
	    padding-top: 10px;
	}
	
	.line.line2 {
	    height: 15px;
	    line-height: 15px;
	}
	
	.line.line3 {
	    height: 12px;
	    line-height: 12px;
	}
	
	button[type="primary"] {
	    background: #588aff;
	}
	
	.button-hover[type="primary"],button[type="primary"]:active {
	    background: #73a8ff;
	}
	
	.listr {
	    padding: 0 0 0 15px;
	}
	
	.listr,.listr .d1 {
	    box-sizing: border-box;
	}
	
	.listr .d1 {
	    height: 45px;
	    line-height: 45px;
	    border-bottom: 1rpx solid #eee;
	    font-size: 15px;
	    color: #333;
	}
	
	.listr .d1 .img1 {
	    float: left;
	    width: 21px;
	    height: 21px;
	    margin-top: 12px;
	    margin-right: 5px;
	}
	
	.listr .d1 .t1 {
	    padding-left: 10px;
	    font-size: 12px;
	    color: #bfbfbf;
	}
	
	.listr .d2 {
	    margin-right: 15px;
	    background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/app7.png) no-repeat 100%;
	    background-size: 7px auto;
	    padding-right: 20px;
	    opacity: .7;
	}
	
	.listr .d2,.listr .d3 {
	    float: right;
	    height: 45px;
	    font-size: 13px;
	}
	
	.listr .d3 {
	    padding-right: 35px;
	    background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/18.png) no-repeat 50%;
	    background-size: 17px auto;
	    opacity: .3;
	    width: 10px;
	}
	
	.listr .d_icon {
	    display: flex;
	    align-items: center;
	}
	
	.listr .d_icon .icon {
	    margin-left: 5px;
	}
	
	.listr:active {
	    background-color: #eee;
	}
	
	.lists .listr:last-child .d1 {
	    border-bottom: 0;
	}
	
	.listrbr .d1 {
	    height: auto;
	    overflow: hidden;
	}
	
	.listrbr .d2 {
	    max-width: 550rpx;
	    line-height: 21px;
	    padding-top: 12px;
	    padding-bottom: 12px;
	    height: auto;
	}
	
	.listrswitch .d1 {
	    height: auto;
	    overflow: hidden;
	}
	
	.listrswitch .d2 {
	    background: none;
	    padding-right: 0;
	    display: flex;
	    align-items: center;
	}
	
	.listrswitch .int1 {
	    height: 30px;
	    line-height: 30px;
	    text-align: right;
	}
	
	.m_gui_box,button[type="default"] {
	    background: #fff;
	}
	
	.m_gui_box {
	    position: fixed;
	    box-sizing: border-box;
	    padding: 30rpx;
	    z-index: 999;
	    width: 100%;
	    height: 100%;
	    left: 0;
	    top: 0;
	    overflow: hidden;
	}
	
	.m_gui_logo,.m_gui_logo .img1 {
	    margin: 0 auto;
	    width: 138rpx;
	    height: 138rpx;
	}
	
	.m_gui_logo {
	    padding-top: 55rpx;
	}
	
	.m_gui_logo .img1 {
	    background: #588bff;
	    border-radius: 138rpx;
	}
	
	.m_gui_name {
	    text-align: center;
	    font-size: 36rpx;
	    font-weight: 700;
	    line-height: 36rpx;
	    padding: 30rpx 0 65rpx;
	    border-bottom: 1rpx solid #e2e2e2;
	}
	
	.m_gui_get {
	    font-size: 32rpx;
	    color: #272727;
	    padding: 50rpx 38rpx 20rpx;
	    line-height: 40rpx;
	}
	
	.m_gui_li {
	    line-height: 48rpx;
	    padding: 0 38rpx;
	    font-size: 28rpx;
	    color: #8f8f8f;
	}
	
	.m_gui_li .yuan {
	    display: inline-block;
	    margin-right: 22rpx;
	    width: 8rpx;
	    height: 8rpx;
	    vertical-align: middle;
	    line-height: 0;
	    border-radius: 8rpx;
	    background: #8f8f8f;
	}
	
	.m_gui_button {
	    padding: 75rpx 30rpx 0;
	}
	
	.main_getuserinfo {
	    position: fixed;
	    z-index: 999;
	    width: 100%;
	    height: 100%;
	    left: 0;
	    top: 0;
	    border: 0;
	    border-radius: 0;
	    background: transparent;
	}
	
	.add-yuyin {
	    position: fixed;
	    z-index: 9;
	    background: rgba(0,0,0,.7);
	    border-radius: 20rpx;
	    width: 300rpx;
	    height: 300rpx;
	    top: 50%;
	    left: 50%;
	    margin: -150rpx 0 0 -150rpx;
	}
	
	.add-yuyin .dj1 {
	    display: inline-block;
	    background: ();
	}
	
	.app_xinshou {
	    position: fixed;
	    right: 30rpx;
	    bottom: 60px;
	}
	
	.app_xinshou .img {
	    width: 120rpx;
	}
	
	.icon_wenhao {
	    background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/21.png) no-repeat 50%;
	    background-size: 16px 16px;
	    opacity: .3;
	}
	
	.icon_qrcode,.icon_wenhao {
	    display: inline-block;
	    width: 30px;
	    height: 30px;
	}
	
	.icon_qrcode {
	    background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/32.png) no-repeat 50%;
	    background-size: 16px 16px;
	}
	
	.icon_vip {
	    background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/vip.png) no-repeat 50%;
	    background-size: 25px auto;
	    display: inline-block;
	    width: 35px;
	    height: 30px;
	}
	
	.icon_edit {
	    background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/edit.png) no-repeat 50%;
	    background-size: 12px 12px;
	    display: inline-block;
	    width: 12px;
	    height: 12px;
	}
	
	.icon_rili {
	    background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/11.png) no-repeat 50%;
	    background-size: 16px 16px;
	    width: 16px;
	}
	
	.icon_daiji,.icon_rili {
	    display: inline-block;
	    height: 16px;
	    opacity: .3;
	}
	
	.icon_daiji {
	    background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/daiji.png) no-repeat 50%;
	    background-size: 35px 16px;
	    width: 35px;
	}
	
	.icon_huishan {
	    background: url(https://static-1253713495.file.myqcloud.com/miniapps/jizhang/images/huishan.png) no-repeat 50%;
	    background-size: 24px 24px;
	    display: inline-block;
	    width: 24px;
	    height: 24px;
	    opacity: .8;
	}
	
	.custom_title {
	    padding-left: 15px;
	    align-items: center;
	    color: #fff;
	    box-sizing: border-box;
	}
	
	.custom_title,.custom_title .name {
	    line-height: 24px;
	    display: flex;
	}
	
	.custom_title .name {
	    font-size: 16px;
	    height: 24px;
	    font-weight: 700;
	    max-width: 160px;
	    overflow: hidden;
	    text-overflow: ellipsis;
	    justify-content: flex-start;
	}
	
	.custom_title .goback {
	    display: flex;
	    align-items: center;
	    margin-left: -10px;
	    width: 35px;
	    height: 100%;
	}
	
	.custom_title .goback .icon {
	    height: 25px;
	    width: 25px;
	}
	
	.custom_title .name .icon_vip {
	    height: 24px;
	    width: 25px;
	    min-width: 25px;
	    margin-right: 5px;
	    flex-shrink: 0;
	}
	
	.select_time {
	    position: fixed;
	    top: 0;
	    height: 100%;
	    background-color: transparent;
	    z-index: -1;
	}
	
	.select_time,.select_time .select_time_main {
	    left: 0;
	    width: 100%;
	    transition: all .5s;
	}
	
	.select_time .select_time_main {
	    padding: 15px;
	    box-sizing: border-box;
	    box-shadow: 0 0 30px hsla(0,0%,78.4%,.1);
	    border-top-left-radius: 15px;
	    border-top-right-radius: 15px;
	    background: #fff;
	    position: absolute;
	    bottom: -90%;
	    overflow: hidden;
	}
	
	.select_time.show {
	    background-color: rgba(0,0,0,.1);
	    z-index: 2;
	}
	
	.select_time.show .select_time_main {
	    bottom: 0;
	}
	
	.select_time_main .top {
	    display: flex;
	    flex-wrap: wrap;
	    font-size: 14px;
	}
	
	.select_time_main .top .li {
	    color: #8f8f8f;
	    border-bottom: 2px solid transparent;
	    line-height: 28px;
	    padding: 0 4px;
	    margin-right: 10px;
	}
	
	.select_time_main .top .li.hover {
	    border-color: #588aff;
	    color: #333;
	}
	
	.select_time_main .midd {
	    padding: 20px 0;
	    color: #666;
	}
	
	.select_time_main .midd .scroll {
	    max-height: 200px;
	}
	
	.select_time_main .buttom {
	    display: flex;
	    align-items: center;
	    justify-content: center;
	    padding-bottom: calc(env(safe-area-inset-bottom));
	}
	
	.select_time_main .buttom .button {
	    border: 1px solid hsla(0,0%,39.2%,.1);
	    width: 100px;
	    height: 35px;
	    line-height: 35px;
	    text-align: center;
	    border-radius: 4px;
	}
	
	.select_time_main .buttom .button:first-child {
	    background-color: hsla(0,0%,39.2%,.1);
	}
	
	.select_time_main .buttom .button:last-child {
	    background-color: #588aff;
	    color: #fff;
	    margin-left: 20px;
	}
	
	.select_time_main .buttom .button:active {
	    opacity: .9;
	}
	
	.select_time_main .midd .year .li {
	    margin-bottom: 10px;
	    padding: 5px 15px;
	    border-radius: 2px;
	    border: 1px solid hsla(0,0%,39.2%,.1);
	}
	
	.select_time_main .midd .year .li.hover {
	    background: rgba(88,138,255,.1);
	    color: rgba(88,138,255,.9);
	    border-color: rgba(88,138,255,.5);
	}
	
	.select_time_main .midd .month {
	    display: flex;
	    flex-wrap: wrap;
	    flex-direction: row;
	    justify-content: space-between;
	}
	
	.select_time_main .midd .month .li {
	    width: 31%;
	    text-align: center;
	    box-sizing: border-box;
	    margin-bottom: 10px;
	    padding: 5px 15px;
	    border-radius: 2px;
	    border: 1px solid hsla(0,0%,39.2%,.1);
	}
	
	.select_time_main .midd .month .li.hover {
	    background: rgba(88,138,255,.1);
	    color: rgba(88,138,255,.9);
	    border-color: rgba(88,138,255,.5);
	}
	
	.select_time_main .midd .zdy {
	    display: flex;
	    justify-content: center;
	    align-items: center;
	    height: 200px;
	}
	
	.select_time_main .midd .zdy .box2 {
	    width: 100%;
	    box-sizing: border-box;
	    width: 250px;
	}
	
	.select_time_main .midd .zdy .dao {
	    text-align: center;
	    padding: 20px 0 10px;
	}
	
	.select_time_main .midd .zdy .int1 {
	    width: 100%;
	    height: 45px;
	    line-height: 45px;
	    box-sizing: border-box;
	    border: none;
	    border-bottom: 1px solid rgba(0,0,0,.1);
	    text-align: center;
	}
	
	.select_time_main .midd .month,.select_time_main .midd .year,.select_time_main .midd .zdy {
	    display: none;
	}
	
	.select_time_main .midd .year.show {
	    display: block;
	}
	
	.select_time_main .midd .month.show,.select_time_main .midd .zdy.show {
	    display: flex;
	}
	
	.change_book_box {
	    position: fixed;
	    top: 0;
	    left: 0;
	    width: 100%;
	    height: 100%;
	    background-color: transparent;
	    z-index: -1;
	    transition: all .3s;
	}
	
	.change_book_box .change_book {
	    box-sizing: border-box;
	    box-shadow: 0 0 30px hsla(0,0%,78.4%,.1);
	    border-top-left-radius: 15px;
	    border-top-right-radius: 15px;
	    background: #fff;
	    position: absolute;
	    width: 100%;
	    left: 0;
	    bottom: -160%;
	    overflow: hidden;
	    transition: bottom .3s;
	    padding: 0 15px calc(30px + env(safe-area-inset-bottom));
	}
	
	.change_book_box .change_book .list {
	    display: flex;
	    justify-content: space-between;
	    color: rgba(0,0,0,.7);
	    margin-top: 10px;
	    padding: 9px 15px;
	    border-radius: 3px;
	    border: 1px solid rgba(0,0,0,.1);
	}
	
	.change_book_box .change_book .list .r {
	    color: #fff;
	    font-size: 11px;
	    background-color: #588bff;
	    border-radius: 15px;
	    line-height: 22px;
	    padding: 0 12px;
	}
	
	.change_book_box .change_book .change_book_title {
	    display: flex;
	    justify-content: space-between;
	}
	
	.change_book_box .change_book .change_book_title .t1,.change_book_box .change_book .change_book_title .t2 {
	    color: hsla(0,0%,39.2%,.7);
	    display: inline-block;
	    padding: 15px 0 5px;
	    height: 30px;
	    line-height: 30px;
	    font-size: 14px;
	}
	
	.change_book_box .change_book .list:active {
	    background-color: hsla(0,0%,39.2%,.1);
	}
	
	.change_book_box .change_book .list.hover {
	    color: #588bff;
	    border-color: #588bff;
	    background-color: rgba(88,139,255,.1);
	}
	
	.change_book_box.show {
	    background-color: rgba(0,0,0,.2);
	    z-index: 10;
	}
	
	.change_book_box.show .change_book {
	    bottom: 0;
	}
	
	.change_book_scroll {
	    max-height: 350px;
	}
	
	.change_book_box .change_book .list .l .icon_vip {
	    width: 25px;
	    height: 11px;
	    margin: 0 5px;
	}
	
	.crad_box {
	    box-sizing: border-box;
	    border: 1px solid hsla(0,0%,39.2%,.1);
	    background-color: #588bff;
	    background-image: linear-gradient(160deg,#7397ff 20%,#588bff 80%);
	    color: #fff;
	    border-radius: 5px;
	    padding: 15px;
	}
	
	.flag_list_box {
	    font-size: 28rpx;
	    margin-top: 30rpx;
	}
	
	.flag_list_box .border {
	    box-shadow: 0 0 10rpx rgba(0,0,0,.1);
	    border-radius: 10rpx;
	    border: 1rpx solid hsla(0,0%,100%,.1);
	    background-color: #fff;
	    background-image: linear-gradient(180deg,#6a97ff 20%,#588aff 80%);
	}
	
	.flag_list_box .f_top {
	    padding: 20rpx;
	    color: hsla(0,0%,100%,.8);
	    justify-content: space-between;
	    font-size: 24rpx;
	}
	
	.flag_list_box .f_top,.flag_list_box .f_top .l,.flag_list_box .f_top .r {
	    display: flex;
	    align-items: center;
	}
	
	.flag_list_box .f_top .type {
	    box-shadow: 0 0 5rpx hsla(0,0%,39.2%,.3);
	    background: #cdc6ac;
	    display: inline-block;
	    font-size: 20rpx;
	    line-height: 35rpx;
	    width: 70rpx;
	    text-align: center;
	    border-radius: 90rpx;
	    border: 1rpx solid hsla(0,0%,39.2%,.4);
	    color: #fff;
	    margin-right: 10rpx;
	    box-sizing: border-box;
	}
	
	.flag_list_box .f_top .type0 {
	    background-color: #cdacca;
	}
	
	.flag_list_box .f_jl {
	    text-align: center;
	    padding: 0 0 10rpx;
	}
	
	.flag_list_box .f_jl .bg {
	    display: inline-block;
	    font-size: 24prx;
	    color: hsla(0,0%,100%,.8);
	    padding: 5rpx 30rpx;
	    border-radius: 90rpx;
	    background-color: hsla(0,0%,100%,.1);
	}
	
	.flag_list_box .f_mid {
	    display: flex;
	    padding: 0 20rpx 40rpx 10rpx;
	}
	
	.flag_list_box .f_mid .d1 {
	    flex: 1;
	    text-align: center;
	    display: flex;
	    justify-content: center;
	    align-items: center;
	}
	
	.flag_list_box .f_mid .d1 .v1 {
	    font-size: 48rpx;
	    line-height: 55rpx;
	    color: #fff;
	    font-weight: 700;
	}
	
	.flag_list_box .f_mid .d1 .v2 {
	    color: hsla(0,0%,100%,.8);
	    font-size: 24rpx;
	}
	
	.flag_list_box .f_bot {
	    background-color: #fff;
	    overflow: hidden;
	    margin: 0 20rpx;
	    border: 1rpx solid hsla(0,0%,39.2%,.1);
	    border-top: none;
	    border-bottom-left-radius: 6rpx;
	    border-bottom-right-radius: 6rpx;
	    box-sizing: border-box;
	    font-size: 24rpx;
	    line-height: 30rpx;
	}
	
	.flag_list_box .f_bot .tline {
	    display: flex;
	    justify-content: space-between;
	    padding: 10rpx 15rpx;
	    color: rgba(0,0,0,.4);
	}
	
	.loadingbox .loading {
	    height: 2rpx;
	    width: 40%;
	    background: #588aff;
	    opacity: .6;
	    border-radius: 6rpx;
	    animation-name: bulePulse;
	    animation-duration: 2s;
	    animation-iteration-count: infinite;
	}
	
	.percentage {
	    border-radius: 60rpx;
	    width: 120rpx;
	    height: 120rpx;
	    position: relative;
	    margin: 0 auto;
	    overflow: hidden;
	    font-size: 0;
	    line-height: 0;
	    transform: scale(1.2);
	}
	
	.percentage,.percentage .progress {
	    box-shadow: 0 0 5rpx hsla(0,0%,39.2%,.3);
	}
	
	.percentage .progress {
	    position: absolute;
	    border: 1rpx solid hsla(0,0%,100%,.1);
	    box-sizing: border-box;
	    width: 90rpx;
	    height: 90rpx;
	    background-color: #588aff;
	    border-radius: 50rpx;
	    left: 15rpx;
	    top: 15rpx;
	    display: flex;
	    justify-content: center;
	    align-items: center;
	    font-size: 28rpx;
	    color: #fff;
	    line-height: 25rpx;
	}
	
	.percentage .progress .txt {
	    font-size: 16rpx;
	    font-weight: 400;
	}
	
	.percentage .left,.percentage .right {
	    width: 60rpx;
	    height: 120rpx;
	    overflow: hidden;
	    position: relative;
	    float: left;
	    background-color: #ffc060;
	}
	
	.percentage .left {
	    border-radius: 120rpx 0 0 120rpx;
	}
	
	.percentage .right {
	    border-radius: 0 120rpx 120rpx 0;
	}
	
	.percentage .left:after,.percentage .right:after {
	    content: "";
	    position: absolute;
	    display: block;
	    width: 60rpx;
	    height: 120rpx;
	    background-color: #fff;
	    border-radius: 120rpx 0 0 120rpx;
	    background-color: hsla(0,0%,100%,.7);
	}
	
	.percentage .right:after {
	    content: "";
	    position: absolute;
	    display: block;
	    border-radius: 0 120rpx 120rpx 0;
	}
	
	.percentage .left:after {
	    transform-origin: right center;
	}
	
	.percentage .right:after {
	    transform-origin: left center;
	}
	
	.percentage .left0:after,.percentage .right0:after {
	    transform: rotateZ(0deg);
	}
	
	.percentage .right1:after {
	    transform: rotateZ(-1.8deg);
	}
	
	.percentage .left1:after {
	    transform: rotateZ(1.8deg);
	}
	
	.percentage .right2:after {
	    transform: rotateZ(-3.6deg);
	}
	
	.percentage .left2:after {
	    transform: rotateZ(3.6deg);
	}
	
	.percentage .right3:after {
	    transform: rotateZ(-5.4deg);
	}
	
	.percentage .left3:after {
	    transform: rotateZ(5.4deg);
	}
	
	.percentage .right4:after {
	    transform: rotateZ(-7.2deg);
	}
	
	.percentage .left4:after {
	    transform: rotateZ(7.2deg);
	}
	
	.percentage .right5:after {
	    transform: rotateZ(-9deg);
	}
	
	.percentage .left5:after {
	    transform: rotateZ(9deg);
	}
	
	.percentage .right6:after {
	    transform: rotateZ(-10.8deg);
	}
	
	.percentage .left6:after {
	    transform: rotateZ(10.8deg);
	}
	
	.percentage .right7:after {
	    transform: rotateZ(-12.6deg);
	}
	
	.percentage .left7:after {
	    transform: rotateZ(12.6deg);
	}
	
	.percentage .right8:after {
	    transform: rotateZ(-14.4deg);
	}
	
	.percentage .left8:after {
	    transform: rotateZ(14.4deg);
	}
	
	.percentage .right9:after {
	    transform: rotateZ(-16.2deg);
	}
	
	.percentage .left9:after {
	    transform: rotateZ(16.2deg);
	}
	
	.percentage .right10:after {
	    transform: rotateZ(-18deg);
	}
	
	.percentage .left10:after {
	    transform: rotateZ(18deg);
	}
	
	.percentage .right11:after {
	    transform: rotateZ(-19.8deg);
	}
	
	.percentage .left11:after {
	    transform: rotateZ(19.8deg);
	}
	
	.percentage .right12:after {
	    transform: rotateZ(-21.6deg);
	}
	
	.percentage .left12:after {
	    transform: rotateZ(21.6deg);
	}
	
	.percentage .right13:after {
	    transform: rotateZ(-23.4deg);
	}
	
	.percentage .left13:after {
	    transform: rotateZ(23.4deg);
	}
	
	.percentage .right14:after {
	    transform: rotateZ(-25.2deg);
	}
	
	.percentage .left14:after {
	    transform: rotateZ(25.2deg);
	}
	
	.percentage .right15:after {
	    transform: rotateZ(-27deg);
	}
	
	.percentage .left15:after {
	    transform: rotateZ(27deg);
	}
	
	.percentage .right16:after {
	    transform: rotateZ(-28.8deg);
	}
	
	.percentage .left16:after {
	    transform: rotateZ(28.8deg);
	}
	
	.percentage .right17:after {
	    transform: rotateZ(-30.6deg);
	}
	
	.percentage .left17:after {
	    transform: rotateZ(30.6deg);
	}
	
	.percentage .right18:after {
	    transform: rotateZ(-32.4deg);
	}
	
	.percentage .left18:after {
	    transform: rotateZ(32.4deg);
	}
	
	.percentage .right19:after {
	    transform: rotateZ(-34.2deg);
	}
	
	.percentage .left19:after {
	    transform: rotateZ(34.2deg);
	}
	
	.percentage .right20:after {
	    transform: rotateZ(-36deg);
	}
	
	.percentage .left20:after {
	    transform: rotateZ(36deg);
	}
	
	.percentage .right21:after {
	    transform: rotateZ(-37.8deg);
	}
	
	.percentage .left21:after {
	    transform: rotateZ(37.8deg);
	}
	
	.percentage .right22:after {
	    transform: rotateZ(-39.6deg);
	}
	
	.percentage .left22:after {
	    transform: rotateZ(39.6deg);
	}
	
	.percentage .right23:after {
	    transform: rotateZ(-41.4deg);
	}
	
	.percentage .left23:after {
	    transform: rotateZ(41.4deg);
	}
	
	.percentage .right24:after {
	    transform: rotateZ(-43.2deg);
	}
	
	.percentage .left24:after {
	    transform: rotateZ(43.2deg);
	}
	
	.percentage .right25:after {
	    transform: rotateZ(-45deg);
	}
	
	.percentage .left25:after {
	    transform: rotateZ(45deg);
	}
	
	.percentage .right26:after {
	    transform: rotateZ(-46.8deg);
	}
	
	.percentage .left26:after {
	    transform: rotateZ(46.8deg);
	}
	
	.percentage .right27:after {
	    transform: rotateZ(-48.6deg);
	}
	
	.percentage .left27:after {
	    transform: rotateZ(48.6deg);
	}
	
	.percentage .right28:after {
	    transform: rotateZ(-50.4deg);
	}
	
	.percentage .left28:after {
	    transform: rotateZ(50.4deg);
	}
	
	.percentage .right29:after {
	    transform: rotateZ(-52.2deg);
	}
	
	.percentage .left29:after {
	    transform: rotateZ(52.2deg);
	}
	
	.percentage .right30:after {
	    transform: rotateZ(-54deg);
	}
	
	.percentage .left30:after {
	    transform: rotateZ(54deg);
	}
	
	.percentage .right31:after {
	    transform: rotateZ(-55.8deg);
	}
	
	.percentage .left31:after {
	    transform: rotateZ(55.8deg);
	}
	
	.percentage .right32:after {
	    transform: rotateZ(-57.6deg);
	}
	
	.percentage .left32:after {
	    transform: rotateZ(57.6deg);
	}
	
	.percentage .right33:after {
	    transform: rotateZ(-59.4deg);
	}
	
	.percentage .left33:after {
	    transform: rotateZ(59.4deg);
	}
	
	.percentage .right34:after {
	    transform: rotateZ(-61.2deg);
	}
	
	.percentage .left34:after {
	    transform: rotateZ(61.2deg);
	}
	
	.percentage .right35:after {
	    transform: rotateZ(-63deg);
	}
	
	.percentage .left35:after {
	    transform: rotateZ(63deg);
	}
	
	.percentage .right36:after {
	    transform: rotateZ(-64.8deg);
	}
	
	.percentage .left36:after {
	    transform: rotateZ(64.8deg);
	}
	
	.percentage .right37:after {
	    transform: rotateZ(-66.6deg);
	}
	
	.percentage .left37:after {
	    transform: rotateZ(66.6deg);
	}
	
	.percentage .right38:after {
	    transform: rotateZ(-68.4deg);
	}
	
	.percentage .left38:after {
	    transform: rotateZ(68.4deg);
	}
	
	.percentage .right39:after {
	    transform: rotateZ(-70.2deg);
	}
	
	.percentage .left39:after {
	    transform: rotateZ(70.2deg);
	}
	
	.percentage .right40:after {
	    transform: rotateZ(-72deg);
	}
	
	.percentage .left40:after {
	    transform: rotateZ(72deg);
	}
	
	.percentage .right41:after {
	    transform: rotateZ(-73.8deg);
	}
	
	.percentage .left41:after {
	    transform: rotateZ(73.8deg);
	}
	
	.percentage .right42:after {
	    transform: rotateZ(-75.6deg);
	}
	
	.percentage .left42:after {
	    transform: rotateZ(75.6deg);
	}
	
	.percentage .right43:after {
	    transform: rotateZ(-77.4deg);
	}
	
	.percentage .left43:after {
	    transform: rotateZ(77.4deg);
	}
	
	.percentage .right44:after {
	    transform: rotateZ(-79.2deg);
	}
	
	.percentage .left44:after {
	    transform: rotateZ(79.2deg);
	}
	
	.percentage .right45:after {
	    transform: rotateZ(-81deg);
	}
	
	.percentage .left45:after {
	    transform: rotateZ(81deg);
	}
	
	.percentage .right46:after {
	    transform: rotateZ(-82.8deg);
	}
	
	.percentage .left46:after {
	    transform: rotateZ(82.8deg);
	}
	
	.percentage .right47:after {
	    transform: rotateZ(-84.6deg);
	}
	
	.percentage .left47:after {
	    transform: rotateZ(84.6deg);
	}
	
	.percentage .right48:after {
	    transform: rotateZ(-86.4deg);
	}
	
	.percentage .left48:after {
	    transform: rotateZ(86.4deg);
	}
	
	.percentage .right49:after {
	    transform: rotateZ(-88.2deg);
	}
	
	.percentage .left49:after {
	    transform: rotateZ(88.2deg);
	}
	
	.percentage .right50:after {
	    transform: rotateZ(-90deg);
	}
	
	.percentage .left50:after {
	    transform: rotateZ(90deg);
	}
	
	.percentage .right51:after {
	    transform: rotateZ(-91.8deg);
	}
	
	.percentage .left51:after {
	    transform: rotateZ(91.8deg);
	}
	
	.percentage .right52:after {
	    transform: rotateZ(-93.6deg);
	}
	
	.percentage .left52:after {
	    transform: rotateZ(93.6deg);
	}
	
	.percentage .right53:after {
	    transform: rotateZ(-95.4deg);
	}
	
	.percentage .left53:after {
	    transform: rotateZ(95.4deg);
	}
	
	.percentage .right54:after {
	    transform: rotateZ(-97.2deg);
	}
	
	.percentage .left54:after {
	    transform: rotateZ(97.2deg);
	}
	
	.percentage .right55:after {
	    transform: rotateZ(-99deg);
	}
	
	.percentage .left55:after {
	    transform: rotateZ(99deg);
	}
	
	.percentage .right56:after {
	    transform: rotateZ(-100.8deg);
	}
	
	.percentage .left56:after {
	    transform: rotateZ(100.8deg);
	}
	
	.percentage .right57:after {
	    transform: rotateZ(-102.6deg);
	}
	
	.percentage .left57:after {
	    transform: rotateZ(102.6deg);
	}
	
	.percentage .right58:after {
	    transform: rotateZ(-104.4deg);
	}
	
	.percentage .left58:after {
	    transform: rotateZ(104.4deg);
	}
	
	.percentage .right59:after {
	    transform: rotateZ(-106.2deg);
	}
	
	.percentage .left59:after {
	    transform: rotateZ(106.2deg);
	}
	
	.percentage .right60:after {
	    transform: rotateZ(-108deg);
	}
	
	.percentage .left60:after {
	    transform: rotateZ(108deg);
	}
	
	.percentage .right61:after {
	    transform: rotateZ(-109.8deg);
	}
	
	.percentage .left61:after {
	    transform: rotateZ(109.8deg);
	}
	
	.percentage .right62:after {
	    transform: rotateZ(-.31turn);
	}
	
	.percentage .left62:after {
	    transform: rotateZ(.31turn);
	}
	
	.percentage .right63:after {
	    transform: rotateZ(-113.4deg);
	}
	
	.percentage .left63:after {
	    transform: rotateZ(113.4deg);
	}
	
	.percentage .right64:after {
	    transform: rotateZ(-.32turn);
	}
	
	.percentage .left64:after {
	    transform: rotateZ(.32turn);
	}
	
	.percentage .right65:after {
	    transform: rotateZ(-117deg);
	}
	
	.percentage .left65:after {
	    transform: rotateZ(117deg);
	}
	
	.percentage .right66:after {
	    transform: rotateZ(-.33turn);
	}
	
	.percentage .left66:after {
	    transform: rotateZ(.33turn);
	}
	
	.percentage .right67:after {
	    transform: rotateZ(-120.6deg);
	}
	
	.percentage .left67:after {
	    transform: rotateZ(120.6deg);
	}
	
	.percentage .right68:after {
	    transform: rotateZ(-.34turn);
	}
	
	.percentage .left68:after {
	    transform: rotateZ(.34turn);
	}
	
	.percentage .right69:after {
	    transform: rotateZ(-124.2deg);
	}
	
	.percentage .left69:after {
	    transform: rotateZ(124.2deg);
	}
	
	.percentage .right70:after {
	    transform: rotateZ(-126deg);
	}
	
	.percentage .left70:after {
	    transform: rotateZ(126deg);
	}
	
	.percentage .right71:after {
	    transform: rotateZ(-127.8deg);
	}
	
	.percentage .left71:after {
	    transform: rotateZ(127.8deg);
	}
	
	.percentage .right72:after {
	    transform: rotateZ(-.36turn);
	}
	
	.percentage .left72:after {
	    transform: rotateZ(.36turn);
	}
	
	.percentage .right73:after {
	    transform: rotateZ(-131.4deg);
	}
	
	.percentage .left73:after {
	    transform: rotateZ(131.4deg);
	}
	
	.percentage .right74:after {
	    transform: rotateZ(-.37turn);
	}
	
	.percentage .left74:after {
	    transform: rotateZ(.37turn);
	}
	
	.percentage .right75:after {
	    transform: rotateZ(-135deg);
	}
	
	.percentage .left75:after {
	    transform: rotateZ(135deg);
	}
	
	.percentage .right76:after {
	    transform: rotateZ(-.38turn);
	}
	
	.percentage .left76:after {
	    transform: rotateZ(.38turn);
	}
	
	.percentage .right77:after {
	    transform: rotateZ(-138.6deg);
	}
	
	.percentage .left77:after {
	    transform: rotateZ(138.6deg);
	}
	
	.percentage .right78:after {
	    transform: rotateZ(-.39turn);
	}
	
	.percentage .left78:after {
	    transform: rotateZ(.39turn);
	}
	
	.percentage .right79:after {
	    transform: rotateZ(-142.2deg);
	}
	
	.percentage .left79:after {
	    transform: rotateZ(142.2deg);
	}
	
	.percentage .right80:after {
	    transform: rotateZ(-144deg);
	}
	
	.percentage .left80:after {
	    transform: rotateZ(144deg);
	}
	
	.percentage .right81:after {
	    transform: rotateZ(-145.8deg);
	}
	
	.percentage .left81:after {
	    transform: rotateZ(145.8deg);
	}
	
	.percentage .right82:after {
	    transform: rotateZ(-.41turn);
	}
	
	.percentage .left82:after {
	    transform: rotateZ(.41turn);
	}
	
	.percentage .right83:after {
	    transform: rotateZ(-149.4deg);
	}
	
	.percentage .left83:after {
	    transform: rotateZ(149.4deg);
	}
	
	.percentage .right84:after {
	    transform: rotateZ(-.42turn);
	}
	
	.percentage .left84:after {
	    transform: rotateZ(.42turn);
	}
	
	.percentage .right85:after {
	    transform: rotateZ(-153deg);
	}
	
	.percentage .left85:after {
	    transform: rotateZ(153deg);
	}
	
	.percentage .right86:after {
	    transform: rotateZ(-154.8deg);
	}
	
	.percentage .left86:after {
	    transform: rotateZ(154.8deg);
	}
	
	.percentage .right87:after {
	    transform: rotateZ(-156.6deg);
	}
	
	.percentage .left87:after {
	    transform: rotateZ(156.6deg);
	}
	
	.percentage .right88:after {
	    transform: rotateZ(-.44turn);
	}
	
	.percentage .left88:after {
	    transform: rotateZ(.44turn);
	}
	
	.percentage .right89:after {
	    transform: rotateZ(-160.2deg);
	}
	
	.percentage .left89:after {
	    transform: rotateZ(160.2deg);
	}
	
	.percentage .right90:after {
	    transform: rotateZ(-162deg);
	}
	
	.percentage .left90:after {
	    transform: rotateZ(162deg);
	}
	
	.percentage .right91:after {
	    transform: rotateZ(-163.8deg);
	}
	
	.percentage .left91:after {
	    transform: rotateZ(163.8deg);
	}
	
	.percentage .right92:after {
	    transform: rotateZ(-165.6deg);
	}
	
	.percentage .left92:after {
	    transform: rotateZ(165.6deg);
	}
	
	.percentage .right93:after {
	    transform: rotateZ(-167.4deg);
	}
	
	.percentage .left93:after {
	    transform: rotateZ(167.4deg);
	}
	
	.percentage .right94:after {
	    transform: rotateZ(-.47turn);
	}
	
	.percentage .left94:after {
	    transform: rotateZ(.47turn);
	}
	
	.percentage .right95:after {
	    transform: rotateZ(-171deg);
	}
	
	.percentage .left95:after {
	    transform: rotateZ(171deg);
	}
	
	.percentage .right96:after {
	    transform: rotateZ(-172.8deg);
	}
	
	.percentage .left96:after {
	    transform: rotateZ(172.8deg);
	}
	
	.percentage .right97:after {
	    transform: rotateZ(-174.6deg);
	}
	
	.percentage .left97:after {
	    transform: rotateZ(174.6deg);
	}
	
	.percentage .right98:after {
	    transform: rotateZ(-.49turn);
	}
	
	.percentage .left98:after {
	    transform: rotateZ(.49turn);
	}
	
	.percentage .right99:after {
	    transform: rotateZ(-178.2deg);
	}
	
	.percentage .left99:after {
	    transform: rotateZ(178.2deg);
	}
	
	.percentage .right100:after {
	    transform: rotateZ(-180deg);
	}
	
	.percentage .left100:after {
	    transform: rotateZ(180deg);
	}
</style>
