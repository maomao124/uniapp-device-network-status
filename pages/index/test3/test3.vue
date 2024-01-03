<template>
	<view>
		<button type="primary" @click="button1">获取网络类型</button>
		<button type="primary" @click="button2">监听网络状态变化</button>
		<button type="primary" @click="button3">取消监听网络状态变化</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				f:undefined
			}
		},
		methods: {
			button1()
			{
				uni.getNetworkType({
					success: (res) => {
						console.log(res);
						console.log(res.networkType);
						uni.showModal({
							title:'提示',
							content:'当前网络类型为：'+res.networkType,
							showCancel:false,
						})
					},
					fail: (err) => {
						console.log('获取网络类型失败');
					}
				})
			},
			button2()
			{
				if(!this.f)
				{
					console.log("监听网络状态变化");
					this.f=function(res)
					{
						console.log(res.isConnected);
						console.log(res.networkType);
						uni.showModal({
							title:'提示',
							content:'监听到当前网络类型为：'+ res.networkType+',连接状态：'+res.isConnected,
							showCancel:false,
						})
					}
					uni.onNetworkStatusChange(this.f)
				}
			},
			button3()
			{
				if(this.f)
				{
					console.log("取消监听网络状态变化");
					uni.offNetworkStatusChange(this.f);
					this.f=undefined;
				}
			}
		}
	}
</script>

<style>
button{
	margin: 5px;
}
</style>
