<template>
	<view>
		<button type="primary" @click="button1">获取网络类型</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
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
			}
		}
	}
</script>

<style>

</style>
