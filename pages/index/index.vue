<template>
	<view>
		<view class="grid col-3 padding-sm" style='180upx'>
			<view class="padding-xs animation-scale-down" v-for="(item, index) in btnList" :key='index' @click="changeViewFun(index)">
				<view class="padding radius text-center shadow-blur" :class="changeView===index?'bg-gradual-purple':item.color">
					<view class="text-lg cuIcon" :class='item.iconType'></view>
					<view class="margin-top-sm text-Abc">{{item.type}}</view>
				</view>
			</view>
			<!-- <view class="padding-xs">
				<view class="bg-gradual-blue padding radius text-center shadow-blur">
					<view class="text-lg cuIcon cuIcon-mail"></view>
					<view class="margin-top-sm text-Abc">分类查看</view>
				</view>
			</view>
			<view class="padding-xs">
				<view class="bg-gradual-purple padding radius text-center shadow-blur">
					<view class="text-lg cuIcon cuIcon-mail"></view>
					<view class="margin-top-sm text-Abc">在线地图</view>
				</view>
			</view> -->
		</view>
		<!-- 垂直导航 分区查找 -->
		<view class="VerticalBox" v-if='changeView===0'>
			<scroll-view class="VerticalNav nav" scroll-y scroll-with-animation :scroll-top="verticalNavTop" style="height:calc(100vh - 250upx)">
				<view class="cu-item" :class="index==tabCur?'text-green cur':''" v-for="(item,index) in list" :key="index" @tap="TabSelect"
				 :data-id="index">
					区域{{item.name}}
				</view>
			</scroll-view>
			<scroll-view class="VerticalMain" scroll-y scroll-with-animation style="height:calc(100vh - 250upx)"
			 :scroll-into-view="'main-'+mainCur" @scroll="VerticalMain">
				<view class="padding-top padding-lr" v-for="(item,index) in list" :key="index" :id="'main-'+index">
					<view class="cu-bar solid-bottom bg-white">
						<view class="action">
							<text class="cuIcon-title text-green"></text> 区域{{item.name}}</view>
					</view>
					<view class="cu-list menu-avatar">
						<view class="cu-item" v-for="(sbmsg,index) in msglist" :key='index' :class='sbmsg.isOpen?"cur":"grayscale"'>
							<!-- <view class="cu-avatar round lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg);"></view> -->
							<view class="cu-avatar round lg">
								<text class='cuIcon cuIcon-paint'></text>
							</view>
							<view class="content">
								<!-- <view class="text-grey sbname">{{sbmsg.name}}</view> -->
								<view class="text-grey"><text class="text-cut sbname">{{sbmsg.name}}</text></view>
								<view class="text-gray text-sm flex">
									<view class="cu-tag round bg-orange sm">{{sbmsg.type}}</view>
									<!-- <text class="text-cut">
										<text class="cuIcon-infofill text-red  margin-right-xs"></text>
										{{sbmsg.type}}
									</text>--> 
									</view> 
							</view>
							<view class="action">
								<switch style="transform: scale(0.7,0.7)" @change="SetShadow(sbmsg,index)" :checked="sbmsg.isOpen" :class="shadow?'checked':''" color="#39B54A"></switch>
								<!-- <view class="text-grey text-xs">22:20</view>
								<view class="cu-tag round bg-grey sm">5</view> -->
							</view>
						</view>
						
<!-- 						<view class="cu-item">
							<view class="cu-avatar round lg">
								<text class='cuIcon cuIcon-paint'></text>
							</view>
							<view class="cu-avatar round lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/img/champion/Taric.png);">
								<view class="cu-tag badge">99+</view>
							</view>
							<view class="content">
								<view class="text-grey sbname">
									<text class="text-cut">瓦洛兰之盾-塔里克</text>
									<view class="cu-tag round bg-orange sm">战士</view>
								</view>
								<view class="text-gray text-sm flex">
									<text class="text-cut">
										塔里克是保护者星灵，用超乎寻常的力量守护着符文之地的生命、仁爱以及万物之美。塔里克由于渎职而被放逐，离开了祖国德玛西亚，前去攀登巨神峰寻找救赎，但他找到的却是来自星界的更高层的召唤。现在的塔里克与古代巨神族的神力相融合，以瓦洛兰之盾的身份，永不疲倦地警惕着阴险狡诈的虚空腐化之力。
									</text>
								</view>
							</view>
							<view class="action">
								<view class="text-grey text-xs">22:20</view>
								<view class="cuIcon-notice_forbid_fill text-gray"></view>
							</view>
						</view>
						<view class="cu-item ">
							<view class="cu-avatar round lg">
								<text class='cuIcon cuIcon-paint'></text>
							</view>
							<view class="cu-avatar radius lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/img/champion/Morgana.png);"></view>
							<view class="content">
								<view class="text-pink sbname"><text class="text-cut">莫甘娜</text></view>
								<view class="text-gray text-sm flex"> <text class="text-cut">凯尔，你被自己的光芒变的盲目！</text></view>
							</view>
							<view class="action">
								<view class="text-grey text-xs">22:20</view>
								<view class="cu-tag round bg-red sm">5</view>
							</view>
						</view>
						<view class="cu-item grayscale">
							<view class="cu-avatar round lg">
								<text class='cuIcon cuIcon-paint'></text>
							</view>
							<view class="cu-avatar radius lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81007.jpg);"></view>
							<view class="content">
								<view class='sbname'><text class="text-cut">伊泽瑞尔</text>
									<view class="cu-tag round bg-orange sm">断开连接...</view>
								</view>
								<view class="text-gray text-sm flex"> <text class="text-cut"> 等我回来一个打十个</text></view>
							</view>
							<view class="action">
								<view class="text-grey text-xs">22:20</view>
								<view class="cu-tag round bg-red sm">5</view>
							</view>
						</view>
						<view class="cu-item cur">
							<view class="cu-avatar round lg">
								<text class='cuIcon cuIcon-paint'></text>
							</view>
							<view class="cu-avatar radius lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81020.jpg);">
								<view class="cu-tag badge"></view>
							</view>
							<view class="content">
								<view>
									<text class="text-cut">瓦罗兰大陆-睡衣守护者-新手保护营</text>
									<view class="cu-tag round bg-orange sm">6人</view>
								</view>
								<view class="text-gray text-sm flex">
									<text class="text-cut"> 伊泽瑞尔：<text class="cuIcon-locationfill text-orange margin-right-xs"></text> 传送中...</text></view>
							</view>
							<view class="action">
								<view class="text-grey text-xs">22:20</view>
								<view class="cuIcon-notice_forbid_fill text-gray"></view>
							</view>
						</view> -->
					</view>
				</view>
			</scroll-view>
		</view>
		<!-- 垂直导航 分类查找 -->
		<view class="VerticalBox animation-scale-down" v-else-if="changeView===1">
					<scroll-view class="VerticalNav nav" scroll-y scroll-with-animation :scroll-top="verticalNavTop" style="height:calc(100vh - 250upx)">
						<view class="cu-item" :class="index==tabCur?'text-green cur':''" v-for="(item,index) in list" :key="index" @tap="TabSelect"
						 :data-id="index">
							类型{{item.name}}
						</view>
					</scroll-view>
					<scroll-view class="VerticalMain" scroll-y scroll-with-animation style="height:calc(100vh - 250upx)"
					 :scroll-into-view="'main-'+mainCur" @scroll="VerticalMain">
						<view class="padding-top padding-lr" v-for="(item,index) in list" :key="index" :id="'main-'+index">
							<view class="cu-bar solid-bottom bg-white">
								<view class="action">
									<text class="cuIcon-title text-green"></text> 类型{{item.name}}</view>
							</view>
							<view class="cu-list menu-avatar">
								<view class="cu-item" v-for="(sbmsg,index) in msglist" :key='index' :class='sbmsg.isOpen?"cur":"grayscale"'>
									<!-- <view class="cu-avatar round lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg);"></view> -->
									<view class="cu-avatar round lg">
										<text class='cuIcon cuIcon-paint'></text>
									</view>
									<view class="content">
										<!-- <view class="text-grey sbname">{{sbmsg.name}}</view> -->
										<view class="text-grey"><text class="text-cut sbname">{{sbmsg.name}}</text></view>
										<view class="text-gray text-sm flex">
											<view class="cu-tag round bg-orange sm">{{sbmsg.type}}</view>
											<!-- <text class="text-cut">
												<text class="cuIcon-infofill text-red  margin-right-xs"></text>
												{{sbmsg.type}}
											</text>--> 
											</view> 
									</view>
									<view class="action">
										<switch style="transform: scale(0.7,0.7)" @change="SetShadow(sbmsg,index)" :checked="sbmsg.isOpen" :class="shadow?'checked':''" color="#39B54A"></switch>
										<!-- <view class="text-grey text-xs">22:20</view>
										<view class="cu-tag round bg-grey sm">5</view> -->
									</view>
								</view>
								
		<!-- 						<view class="cu-item">
									<view class="cu-avatar round lg">
										<text class='cuIcon cuIcon-paint'></text>
									</view>
									<view class="cu-avatar round lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/img/champion/Taric.png);">
										<view class="cu-tag badge">99+</view>
									</view>
									<view class="content">
										<view class="text-grey sbname">
											<text class="text-cut">瓦洛兰之盾-塔里克</text>
											<view class="cu-tag round bg-orange sm">战士</view>
										</view>
										<view class="text-gray text-sm flex">
											<text class="text-cut">
												塔里克是保护者星灵，用超乎寻常的力量守护着符文之地的生命、仁爱以及万物之美。塔里克由于渎职而被放逐，离开了祖国德玛西亚，前去攀登巨神峰寻找救赎，但他找到的却是来自星界的更高层的召唤。现在的塔里克与古代巨神族的神力相融合，以瓦洛兰之盾的身份，永不疲倦地警惕着阴险狡诈的虚空腐化之力。
											</text>
										</view>
									</view>
									<view class="action">
										<view class="text-grey text-xs">22:20</view>
										<view class="cuIcon-notice_forbid_fill text-gray"></view>
									</view>
								</view>
								<view class="cu-item ">
									<view class="cu-avatar round lg">
										<text class='cuIcon cuIcon-paint'></text>
									</view>
									<view class="cu-avatar radius lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/img/champion/Morgana.png);"></view>
									<view class="content">
										<view class="text-pink sbname"><text class="text-cut">莫甘娜</text></view>
										<view class="text-gray text-sm flex"> <text class="text-cut">凯尔，你被自己的光芒变的盲目！</text></view>
									</view>
									<view class="action">
										<view class="text-grey text-xs">22:20</view>
										<view class="cu-tag round bg-red sm">5</view>
									</view>
								</view>
								<view class="cu-item grayscale">
									<view class="cu-avatar round lg">
										<text class='cuIcon cuIcon-paint'></text>
									</view>
									<view class="cu-avatar radius lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81007.jpg);"></view>
									<view class="content">
										<view class='sbname'><text class="text-cut">伊泽瑞尔</text>
											<view class="cu-tag round bg-orange sm">断开连接...</view>
										</view>
										<view class="text-gray text-sm flex"> <text class="text-cut"> 等我回来一个打十个</text></view>
									</view>
									<view class="action">
										<view class="text-grey text-xs">22:20</view>
										<view class="cu-tag round bg-red sm">5</view>
									</view>
								</view>
								<view class="cu-item cur">
									<view class="cu-avatar round lg">
										<text class='cuIcon cuIcon-paint'></text>
									</view>
									<view class="cu-avatar radius lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81020.jpg);">
										<view class="cu-tag badge"></view>
									</view>
									<view class="content">
										<view>
											<text class="text-cut">瓦罗兰大陆-睡衣守护者-新手保护营</text>
											<view class="cu-tag round bg-orange sm">6人</view>
										</view>
										<view class="text-gray text-sm flex">
											<text class="text-cut"> 伊泽瑞尔：<text class="cuIcon-locationfill text-orange margin-right-xs"></text> 传送中...</text></view>
									</view>
									<view class="action">
										<view class="text-grey text-xs">22:20</view>
										<view class="cuIcon-notice_forbid_fill text-gray"></view>
									</view>
								</view> -->
							</view>
						</view>
					</scroll-view>
				</view>
				<!-- 地图 -->
				<view v-else-if="changeView===2">
					<mapaa></mapaa>
				</view>
	</view>
</template>

<script>
	import mapaa from '../../components/mapView.vue'
	export default {
		components: {
			mapaa
		},
		data() {
			return {
				// 类型选择
				btnList: [
					{
						type: '分区查看',
						color: 'bg-gradual-green',
						iconType: 'cuIcon-attention'
					},
					{
						type: '分类查看',
						// color: 'bg-gradual-blue',
						color: 'bg-gradual-green',
						iconType: 'cuIcon-mail'
					},
					{
						type: '在线地图',
						// color: 'bg-gradual-purple',
						color: 'bg-gradual-green',
						iconType: 'cuIcon-mail'
					}
				],
				changeView: 0,
				list: [],
				tabCur: 0,
				mainCur: 0,
				verticalNavTop: 0,
				load: true,
				msglist: [
					{
						name: '空气温湿度传感器',
						type: '大气监测',
						isOpen: true
					},
					{
						name: '土壤PH值传感器',
						type: '土壤监测',
						isOpen: true
					},
					{
						name: '叶面温湿度传感器',
						type: '植物监测',
						isOpen: false
					},
					{
						name: '交流自动虫情测报灯',
						type: '虫情监测',
						isOpen: false
					},
					{
						name: '气象站',
						type: '小型监测系统',
						isOpen: true
					},
					{
						name: '网关',
						type: '通讯设备',
						isOpen: false
					}
				]
			};
		},
		onLoad() {
			uni.showLoading({
				title: '加载中...',
				mask: true
			});
			let list = [{}];
			for (let i = 0; i < 26; i++) {
				list[i] = {};
				list[i].name = String.fromCharCode(65 + i);
				list[i].id = i;
			}
			this.list = list;
			this.listCur = list[0];
		},
		onReady() {
			uni.hideLoading()
		},
		methods: {
			/* 修改设备开关状态 */
			SetShadow(e,index) {
				let msg = e.isOpen?'关闭':'打开'
				uni.showModal({
				    title: '警告',
				    content: '确认'+ msg +'此设备',
				    success: res => {
				        if (res.confirm) {
				            console.log('用户点击确定');
							console.log(e)
							e.isOpen = !e.isOpen
							console.log(this.msglist)
							if(e.isOpen === true) {
								uni.showToast({
								    title: '已打开设备',
								    duration: 2000
								});
							}else {
								uni.showToast({
								    title: '已关闭设备',
								    duration: 2000
								});
							}
				        } else if (res.cancel) {
				            console.log('用户点击取消');
				        }
				    }
				});
				
				
			},
			/* 切换类型页面 */
			changeViewFun(e) {
				this.changeView = e
			},
			TabSelect(e) {
				this.tabCur = e.currentTarget.dataset.id;
				this.mainCur = e.currentTarget.dataset.id;
				this.verticalNavTop = (e.currentTarget.dataset.id - 1) * 50
			},
			VerticalMain(e) {
				// #ifdef MP-ALIPAY
				   return false  //支付宝小程序暂时不支持双向联动 
				// #endif
				let that = this;
				let tabHeight = 0;
				console.log(tabHeight)
				if (this.load) {
					for (let i = 0; i < this.list.length; i++) {
						let view = uni.createSelectorQuery().select("#main-" + this.list[i].id);
						view.fields({
							size: true
						}, data => {
							this.list[i].top = tabHeight;
							tabHeight = tabHeight + data.height;
							this.list[i].bottom = tabHeight;
						}).exec();
					}
					this.load = false
				}
				let scrollTop = e.detail.scrollTop + 10;
				for (let i = 0; i < this.list.length; i++) {
					if (scrollTop > this.list[i].top && scrollTop < this.list[i].bottom) {
						this.verticalNavTop = (this.list[i].id - 1) * 50
						this.tabCur = this.list[i].id
						console.log(scrollTop)
						return false
					}
				}
			}
		},
	}
</script>

<style>
	.text-lg{
		font-size:50rpx;
	}
	/* 垂直导航 */
	.fixed {
		position: fixed;
		z-index: 99;
	}
	
	.VerticalNav.nav {
		width: 200upx;
		white-space: initial;
	}
	
	.VerticalNav.nav .cu-item {
		width: 100%;
		text-align: center;
		background-color: #fff;
		margin: 0;
		border: none;
		height: 50px;
		position: relative;
	}
	
	.VerticalNav.nav .cu-item.cur {
		background-color: #f1f1f1;
	}
	
	.VerticalNav.nav .cu-item.cur::after {
		content: "";
		width: 8upx;
		height: 30upx;
		border-radius: 10upx 0 0 10upx;
		position: absolute;
		background-color: currentColor;
		top: 0;
		right: 0upx;
		bottom: 0;
		margin: auto;
	}
	
	.VerticalBox {
		display: flex;
	}
	
	.VerticalMain {
		background-color: #f1f1f1;
		flex: 1;
	}
	.sbname {
		font-size: 20rpx;
	}
</style>
