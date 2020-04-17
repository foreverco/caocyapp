<template>
	<view class="contaiter">
		<view class="welTxt">
			<view>欢迎您</view>
			<view>国草园智慧农业监测平台</view>
		</view>
		<view class="formBox">
			<form action="">
				<view class="loginTitle">
					<view>登 陆</view>
					<view>Sign Up</view>
				</view>
				<view class="cu-form-group">
					<input type="text" v-model="formData.username" placeholder="请输入账号" placeholder-style="color:rgba(39,154,109,0.4)" />
				</view>
				<view class="cu-form-group" id='passInput'>
					<input :type='passType' v-model="formData.password" placeholder="请输入密码" placeholder-style="color:rgba(39,154,109,0.4)" />
					<text :class='passIcon' style="position: absolute;right:70rpx;color:rgba(39,154,109,0.4);z-index: 10001;" @click="changeIcon"></text>
				</view>
				<button type="primary" @click="loginTo">登录</button>
			</form>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			passType:'password',
			passIcon: 'cuIcon-attention',
			formData: {
				username: '',
				password: ''
			}
		};
	},
	methods: {
		changeIcon() {
			console.log(123)
			this.passType === 'password' ? this.passType = 'text' : this.passType = 'password'
			this.passIcon === 'cuIcon-attention' ? this.passIcon = 'cuIcon-attentionforbid' : this.passIcon = 'cuIcon-attention'
		},
		loginTo() {
			if(!this.formData.username){
				uni.showModal({
				    title: '错误',
				    content: '请输入账号',
					showCancel: false,
				    success: function (res) {
				        if (res.confirm) {
				            console.log('用户点击确定');
				        } else if (res.cancel) {
				            console.log('用户点击取消');
				        }
				    }
				});
				return
			}else if (!this.formData.password) {
				uni.showModal({
				    title: '错误',
				    content: '请输入密码',
					showCancel: false,
				    success: function (res) {
				        if (res.confirm) {
				            console.log('用户点击确定');
				        } else if (res.cancel) {
				            console.log('用户点击取消');
				        }
				    }
				})
				return
			}
			uni.reLaunch({
			    url: "../index/index"
			});
			console.log(123)
		}
	}
};
</script>

<style lang="scss">
page {
	background: $login-base64-code;
	background-size: 100% 100%;
}
.contaiter {
	// background: red;
	height: 100vh;
	position: relative;
}
.welTxt {
	// border:1px solid red;
	position: absolute;
	top: 5%;
	height: 10%;
	width: 100%;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-wrap: wrap;
}
.welTxt view {
	width: 100%;
	text-align: center;
	color: #fff;
	font-size: 40rpx;
	letter-spacing: 10rpx;
	font-weight: bold;
}
.formBox {
	position: absolute;
	bottom: 0;
	height: 60%;
	width: 100%;
	display: flex;
	align-items: center;
}
.formBox form {
	height: 80%;
	width: 100%;
	// border:1px solid blue;
	// display: flex;
	// flex-wrap: wrap;
	// align-items: center;
}
.formBox form .loginTitle {
	// border:1px solid red;
}
.formBox form .loginTitle view {
	color: #279a6d;
	display: flex;
	justify-content: center;
	flex-wrap: wrap;
	margin: 10rpx 0;
}
.formBox form .loginTitle view:first-child {
	font-weight: bold;
	font-size: 40rpx;
}
.cu-form-group + .cu-form-group {
	border: 0;
	// width: 70%;
}
#passInput{
	// border:1px solid red;
}

.formBox form input {
	padding-left: 40rpx;
	margin: 50rpx auto;
	height: 100rpx;
	width: 70%;
	border-radius: 100px;
	background: rgba(39, 154, 109, 0.2);
}
.formBox form button {
	width: 50%;
	border-radius: 100px;
}
</style>
