<template>
	<view class="content">
		<view class="art-content"> 
			<rich-text class="richText" :nodes="strings" style="width: 100%; height: 100%;"></rich-text>
			<!-- <object type="text/html" :data="conten_url"  width="100%" height="100%"></object> -->
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '',
				strings: '',
				conten_url: ''
			};
		},
		onLoad: function(e) {
			//console.log(e);
			uni.showLoading({
				title: '加载中...',
				//mask: false
			});
			uni.request({
				url: 'https://news-at.zhihu.com/api/4/news/' + e.id,
				method: 'GET',
				data: {},
				success: res => {
					this.strings = res.data.body;
					this.conten_url = res.data.share_url;
					//console.log(res);
					uni.hideLoading();
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
	.content {
		padding: 10upx 2%;
		width: 96%;
		flex-wrap: wrap;
	}

	.title {
		line-height: 2em;
		font-weight: 700;
		font-size: 38upx;
	}
	.art-content{
		line-height: 1em;
	}

</style>
