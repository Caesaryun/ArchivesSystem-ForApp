
<template>
	<view class="bg">
		<view class="login">
			<image style="margin-left: 7%;width: 240px;height: 70px;margin-top:-10%;" src="../../assets/img/MY-logo.png"></image>
			<view><input type="text" placeholder="用户名" v-model="account" /></view>
			<view><input type="password" placeholder="密码" v-model="password" /></view>
			<view><button type="primary" @tap="login">登录</button></view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				account: "",
				password: "",
				loginForm:{},
			};
		},
		methods: {    //仅先支持管理员登录操作
			login() {
			
				this.loginForm.account = this.account
				this.loginForm.password = this.password
				
		
				uni.request({ 
					url: "http://192.168.43.128:8080/ArchivesSystem/users/login",
					method: "POST",
					// data: {
					// 	username: this.username,
					// 	pwd: this.password
					// },
					data:this.loginForm,
					success: (res) => {
						console.log("登录成功！！！！！！")
						console.log(res)  //还需要保存token信息
						//console.log(res.header.Authorization)
						
						
						if (res.data.code === 200) {
							uni.showToast({
								title: '登录成功',
								duration: 2000
							});
							uni.setStorageSync("account", this.account)
							uni.setStorageSync("token",res.header.Authorization)
							
							console.log("输出保存的jwtToken:" + uni.getStorageSync("token"))
							
							uni.redirectTo({
								url: "../index/main_show"
							});
							
						} else {
							uni.showToast({
								title: '用户名或密码错误',
								icon: "loading",
								duration: 2000
							});
						}
					},

				})
			}
		}
	}
</script>

<style lang="scss">
	.bg {
		background: linear-gradient(to bottom, skyblue, #fff 50%);
		height: 93vh;
		display: flex;
		align-items: center;
		justify-content: center;
		

		.login {
			width: 75vw;
			transform: translateY(-120rpx);
			padding: 20rpx;

			input {
				border: 1rpx solid #C0C0C0;
				border-radius: 10rpx;
				padding: 16rpx;
			}

			view {
				margin: 20rpx 0;
			}

			view:last-of-type {
				margin-top: 40rpx;
			}

			image {
				width: 170rpx;
				height: 170rpx;
				border-radius: 50%;
				margin-left: 35%;
			}
		}
	}
</style>

