<template>
	<view class="content">
		<view class="uni-list">
			<swiper class="banner-image" :indicator-dots="true" :autoplay="true" :interval="2000" :duration="1000">
				<swiper-item  v-for="item in loops" :key="item.id" class="code-image" @tap="openinfo">
					<image  :src="item.image" mode="scaleToFill" ></image>
				</swiper-item>
				
			</swiper>
			
			<view class="uni-media-list-text-bottom uni-ellipsis">今日头条</view>
			<view></view>
			<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in news" :key="index" @tap="openinfo"
			 :data-id="item.id">
				<view class="uni-media-list">
					<image class="uni-media-list-logo" mode="right" :src="item.images"></image>
					<view class="uni-media-list-body">
						<view class="uni-media-list-text-top">{{item.title}}</view>
						<!-- <view class="uni-media-list-text-bottom uni-ellipsis">{{item.content}}</view> -->
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				loops: [],
				news: [],
				img: ''
			};
		},
		onLoad: function() {
			//页面打开显示一些东西
			uni.showLoading({
				title: '加载中...',

			});
			uni.request({
				url: 'https://news-at.zhihu.com/api/4/news/latest',
				method: 'GET',
				data: {},
				success: res => {
					//this.news = res.data.date.stories;
					//console.log(res.data.stories);
					//this.img = res.data.top_stories[0;
					this.loops = res.data.top_stories;
					this.news = res.data.stories;
					console.log(this.loops[0].title);
					uni.hideLoading();

				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			openinfo(e) {
				//获取新闻id
				var id = e.currentTarget.dataset.id;
				//console.log(id);
				uni.navigateTo({
					url: '../info/info?id=' + id,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
	
</script>

<style>
	.uni-media-list-body {
		height: auto;
	}

	.uni-media-list-text-top {
		line-height: 1.6em;
	}
</style>
