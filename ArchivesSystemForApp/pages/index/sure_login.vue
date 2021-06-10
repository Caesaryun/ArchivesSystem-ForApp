<template>

   <view>
      

    <button type="success" @tap="sure_login">确认登录</button>
    <button type="success" @tap="backMain">回到主页</button>
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
			 //确认登录，发送二维码的 tokenId，与shiro的token
			 sure_login(){
				 
				 uni.request({
				 	url: "http://192.168.43.128:8080/ArchivesSystem/common-accessborrow/sure_userinfo?token="+this.token+"&tokenId="+this.tokenId,
				 	method: "POST",
					header:{'Authorization':this.token,
					},
				 	success: (res) => {
				 		
						console.log(res.data)
	
				 		// uni.redirectTo({
				 		// 	url: "../index/main_show"
				 		// });
				 		
				 	},
				 
				 })
			   },
			  //下一个方法
			  backMain(){
				  console.log("回到主页")
				  uni.redirectTo({
				  	url: "../index/main_show"
				  });
			  },
	         /////////
			
		},
			 
			 
			 
}
	
	
	
</script>

<style>
</style>
