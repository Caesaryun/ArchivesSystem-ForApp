<template>
	<view>欢迎来到首页
	      <view> 
		     
		    <button type="primary" @tap="scanQRCode">扫码登录web端</button>
			 
			<h2>二维码携带的Id ： 
			{{tokenId}}</h2>
			<br>
			<h2>shiro认证token: </h2> {{token}}
			<button type="success" @tap="login">回到登录</button>
			
		 </view>
      
    </view>
	
	
</template>

<script>
	export default {
		data() {
			return {
                 url:'',
				 tokenId:'',
				 token:'',
			}
		},
		onLoad() {
            this.tokenId = uni.getStorageSync("tokenId")
			this.token = uni.getStorageSync("token")
		},
		methods: {
			 login(){
				 
				 uni.redirectTo({
				 	url: "../index/login"
				 });
			 },
			 
             scanQRCode(){
				 
				 uni.scanCode({
				     success: function (res) {
				         console.log('条码类型：' + res.scanType);
				         console.log('条码内容：' + res.result);  //其中蕴含网址链接
						
					    console.log("执行访问条码上的链接.....")
						 // http://xxxxxxxxxxxxx/tokenId
						uni.request({
							url: res.result,
							method: "POST",
							success: (res) => {
								console.log(res.data)
								console.log("执行完条码链接又得到了，tokenId")
								uni.setStorageSync("tokenId",res.data)
								this.tokenId = uni.getStorageSync("tokenId")
								console.log("print tokenId:::")
								console.log(this.tokenId)
								
								uni.redirectTo({
									url: "../index/sure_login"
								});
								
							},
						
						})
						 
						 // void plus.runtime.openWeb(res.result,function(){
							//  console.log("跳转操作")
						 // });
						 
				     }
				 });
			 },
			 
		}
	}
</script>

<style lang="scss">

</style>
