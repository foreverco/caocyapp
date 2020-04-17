<template>
	<view>
		<!-- 问题导航 -->
		<scroll-view scroll-x class="bg-green nav text-center">
			<view class="cu-item" :class="0==TabCur?'text-white cur':''" @tap="tabSelect" data-id="0">
				<text class="cuIcon-list" style='margin-right:10rpx'></text> 全部
			</view>
			<view class="cu-item" :class="1==TabCur?'text-white cur':''" @tap="tabSelect" data-id="1">
				<text class="cuIcon-info" style='margin-right:10rpx'></text> 未处理
			</view>
			<view class="cu-item" :class="2==TabCur?'text-white cur':''" @tap="tabSelect" data-id="2">
				<text class="cuIcon-safe" style='margin-right:10rpx'></text> 已处理
			</view>
		</scroll-view>
		<!-- 问题列表 -->
		<view class="cu-bar bg-white solid-bottom margin-top">
			<view class="action">
				<text class="cuIcon-title text-orange "></text> 远程专家-相关问题
			</view>
			<view class="action">
				<button class="cu-btn round bg-green shadow" @click='addQus'>
					<text class="cuIcon-add"></text> 添加</button>
			</view>
		</view>
		<view class="cu-list menu-avatar">
			<view
				class="cu-item"
				:class="modalName == 'move-box-' + index ? 'move-cur' : ''"
				v-for="(item, index) in 10"
				:key="index"
				@touchstart="ListTouchStart"
				@touchmove="ListTouchMove"
				@touchend="ListTouchEnd"
				:data-target="'move-box-' + index"
			>
				<view class="cu-avatar round lg" :style="[{ 
					backgroundImage:index<5? 
					'url(https://ossweb-img.qq.com/images/lol/web201310/skin/big2100' + (index + 2) + '.jpg)' :
					'url(https://ossweb-img.qq.com/images/lol/web201310/skin/big21003.jpg)'
					}]"></view>
				<view class="content">
					<view class="text-grey">文晓港</view>
					<view class="text-gray text-sm">
						<text class="cuIcon-infofill text-red  margin-right-xs"></text>
						消息未送达
					</view>
				</view>
				<view class="action">
					<view class="text-grey text-xs">22:20</view>
					<view class="cu-tag round bg-grey sm">5</view>
				</view>
				<view class="move">
					<view class="bg-grey">置顶</view>
					<view class="bg-red">删除</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			/* 导航 */
			TabCur: 0,
			scrollLeft: 0,
			/* 列表 */
			listTouchStart: 0,
			modalName: null,
		};
	},
	methods: {
		/* 导航 */
		tabSelect(e) {
			this.TabCur = e.currentTarget.dataset.id;
			this.scrollLeft = (e.currentTarget.dataset.id - 1) * 60
		},
		/* 列表 */
		showModal(e) {
			this.modalName = e.currentTarget.dataset.target
		},
		hideModal(e) {
			this.modalName = null
		},
		// ListTouch触摸开始
		ListTouchStart(e) {
			this.listTouchStart = e.touches[0].pageX
		},
		// ListTouch计算方向
		ListTouchMove(e) {
			this.listTouchDirection = e.touches[0].pageX - this.listTouchStart > 0 ? 'right' : 'left'
		},
		
		// ListTouch计算滚动
		ListTouchEnd(e) {
			if (this.listTouchDirection == 'left') {
				this.modalName = e.currentTarget.dataset.target
			} else {
				this.modalName = null
			}
			this.listTouchDirection = null
		},
		/* 添加问题 */
		addQus() {
			uni.navigateTo({
			    url: '/pages/addQuestion/addQuestion'
			});
			console.log(444)
		}
	}
};
</script>

<style></style>
