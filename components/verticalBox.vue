<template>
	<view class="VerticalBox">
			<scroll-view class="VerticalNav nav" scroll-y scroll-with-animation :scroll-top="verticalNavTop" style="height:calc(100vh)">
				<view class="cu-item" :class="index==tabCur?'text-green cur':''" v-for="(item,index) in list" :key="index" @tap="TabSelect"
				 :data-id="index">
					Tab-{{item.name}}
				</view>
			</scroll-view>
			<scroll-view class="VerticalMain" scroll-y scroll-with-animation style="height:calc(100vh)"
			 :scroll-into-view="'main-'+mainCur" @scroll="VerticalMain">
				<view class="padding-top padding-lr" v-for="(item,index) in list" :key="index" :id="'main-'+index">
					<view class="cu-bar solid-bottom bg-white">
						<view class="action">
							<text class="cuIcon-title text-green"></text> 区域-{{item.name}}</view>
					</view>
					<view class="cu-list menu-avatar">
						<view class="cu-item" :class='isOpen?"cur":"grayscale"'>
							<view class="cu-avatar round lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg);"></view>
							<view class="content">
								<view class="text-grey">
									<text class="text-cut sbname">光照强度传感器</text>
								</view>
								<view class="text-gray text-sm flex">
									<view class="cu-tag round bg-orange sm">大气监测</view>
									<!-- <text class="text-cut">
										<text class="cuIcon-infofill text-red  margin-right-xs"></text>
										空气温湿度传感器
									</text> -->
									</view>
							</view>
							<view class="action">
								<switch  style="transform: scale(0.7,0.7)" @change="SetShadow" :checked="isOpen" color="#39B54A"></switch>
								<!-- <view class="text-grey text-xs">22:20</view>
								<view class="cu-tag round bg-grey sm">5</view> -->
							</view>
						</view>
						<view class="cu-item" :class='isOpen?"cur":"grayscale"'>
							<view class="cu-avatar round lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/img/champion/Taric.png);">
								<view class="cu-tag badge">99+</view>
							</view>
							<view class="content">
								<view class="text-grey">
									<text class="text-cut sbname">土壤温湿度传感器</text>
									<!-- <view class="cu-tag round bg-orange sm">土壤监测</view> -->
								</view>
								<view class="text-gray text-sm flex">
									<view class="cu-tag round bg-orange sm">土壤监测</view>
									<!-- <text class="text-cut">
										塔里克是保护者星灵，用超乎寻常的力量守护着符文之地的生命、仁爱以及万物之美。塔里克由于渎职而被放逐，离开了祖国德玛西亚，前去攀登巨神峰寻找救赎，但他找到的却是来自星界的更高层的召唤。现在的塔里克与古代巨神族的神力相融合，以瓦洛兰之盾的身份，永不疲倦地警惕着阴险狡诈的虚空腐化之力。
									</text> -->
								</view>
							</view>
							<view class="action">
								<switch  style="transform: scale(0.7,0.7)" @change="SetShadow" :checked="isOpen" color="#39B54A"></switch>
								<!-- <view class="text-grey text-xs">22:20</view>
								<view class="cuIcon-notice_forbid_fill text-gray"></view> -->
							</view>
						</view>
						<view class="cu-item" :class='!isOpen?"cur":"grayscale"'>
							<view class="cu-avatar radius lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/img/champion/Morgana.png);"></view>
							<view class="content">
								<view class="text-pink"><text class="text-cut sbname">叶面温湿度传感器</text></view>
								<view class="text-gray text-sm flex"> 
								<view class="cu-tag round bg-orange sm">植物监测</view>
								<!-- <text class="text-cut">凯尔，你被自己的光芒变的盲目！</text> -->
								</view>
							</view>
							<view class="action">
								<switch  style="transform: scale(0.7,0.7)" @change="SetShadow" :checked="!isOpen" color="#39B54A"></switch>
								<!-- <view class="text-grey text-xs">22:20</view>
								<view class="cu-tag round bg-red sm">5</view> -->
							</view>
						</view>
						<view class="cu-item" :class='isOpen?"cur":"grayscale"'>
							<view class="cu-avatar radius lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81007.jpg);"></view>
							<view class="content">
								<view><text class="text-cut sbname">气象站</text>
									<!-- <view class="cu-tag round bg-orange sm">断开连接...</view> -->
								</view>
								<view class="text-gray text-sm flex"> 
								<view class="cu-tag round bg-orange sm">小型监测系统</view>
								<!-- <text class="text-cut"> 等我回来一个打十个</text> -->
								</view>
							</view>
							<view class="action">
								<switch  style="transform: scale(0.7,0.7)" @change="SetShadow" :checked="isOpen" color="#39B54A"></switch>
								<!-- <view class="text-grey text-xs">22:20</view>
								<view class="cu-tag round bg-red sm">5</view> -->
							</view>
						</view>
						<view class="cu-item" :class='!isOpen?"cur":"grayscale"'>
							<view class="cu-avatar radius lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big81020.jpg);">
								<view class="cu-tag badge"></view>
							</view>
							<view class="content">
								<view>
									<text class="text-cut sbname">采集器</text>
									<!-- <view class="cu-tag round bg-orange sm">6人</view> -->
								</view>
								<view class="text-gray text-sm flex">
									<view class="cu-tag round bg-orange sm">通讯设备</view>
									<!-- <text class="text-cut"> 伊泽瑞尔：<text class="cuIcon-locationfill text-orange margin-right-xs"></text> 传送中...</text> -->
									</view>
							</view>
							<view class="action">
								<switch  style="transform: scale(0.7,0.7)" @change="SetShadow" :checked="!isOpen" color="#39B54A"></switch>
								<!-- <view class="text-grey text-xs">22:20</view>
								<view class="cuIcon-notice_forbid_fill text-gray"></view> -->
							</view>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [],
				tabCur: 0,
				mainCur: 0,
				verticalNavTop: 0,
				load: true,
				/* 设备是否打开 */
				isOpen:true
			};
		},
		created() {
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
		mounted() {
			uni.hideLoading()
		},
		methods: {
			TabSelect(e) {
				console.log(123)
				this.tabCur = e.currentTarget.dataset.id;
				this.mainCur = e.currentTarget.dataset.id;
				// this.verticalNavTop = (e.currentTarget.dataset.id - 1) * 50
			},
			VerticalMain(e) {
				// #ifdef MP-ALIPAY
				   return false  //支付宝小程序暂时不支持双向联动 
				// #endif
				let that = this;
				let tabHeight = 0;
				console.log(this.load)
				if (this.load) {
					for (let i = 0; i < this.list.length; i++) {
						let view = uni.createSelectorQuery().select("#main-" + this.list[i].id);
						view.fields({
							size: true
						}, data => {
							this.list[i].top = tabHeight;
							tabHeight = tabHeight + data.height;
							this.list[i].bottom = tabHeight;
							console.log(123123123)
						}).exec();
					}
					this.load = false
				}
				let scrollTop = e.detail.scrollTop + 10;
				for (let i = 0; i < this.list.length; i++) {
					console.log(scrollTop)
					console.log(this.list[i].top)
					console.log(this.list[i].bottom)
					console.log(this.list[i])
					if (scrollTop > this.list[i].top && scrollTop < this.list[i].bottom) {
						this.verticalNavTop = (this.list[i].id - 1) * 50
						this.tabCur = this.list[i].id
						console.log(scrollTop)
						return false
					}
				}
			}
		}
	}
</script>

<style>
	/* 垂直导航 */
	.fixed {
		position: fixed;
		z-index: 99;
	}
	.sbname{
		font-size:24rpx;
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
</style>
