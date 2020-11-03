<template>
	<view>
		<view class="title">基本用法</view>
		<view id="normal" class="content" @tap="$refs.normalPopup.open()">点击显示放大popup</view>
		<zwp-blowup-popup ref="normalPopup" selector="normal" @change="onChange">
			<placeholder-text :pNum="2" :lNum="5" />
			<view class="btn" @tap="$refs.normalPopup.close()">点击隐藏</view>
		</zwp-blowup-popup>

		<view class="title">不铺满屏幕</view>
		<view id="nofill" class="content" @tap="$refs.nofillPopup.open()">点击显示放大popup</view>
		<zwp-blowup-popup
			ref="nofillPopup"
			selector="nofill"
			:ani-after-styles="{
				transform: 'translate(20px, 20px)',
				width: 'calc(100vw - 40px)',
				height: 'calc(100vh - 40px)',
				borderRadius: '10px'
			}"
		>
			<placeholder-text :pNum="2" :lNum="5" />
			<view class="btn" @tap="$refs.nofillPopup.close()">点击隐藏</view>
		</zwp-blowup-popup>

		<view class="title">查看大图</view>
		<image id="bigImg" :src="imgSrc" class="small-img" @tap="$refs.bigImgPopup.open()" />
		<zwp-blowup-popup
			ref="bigImgPopup"
			selector="bigImg"
			:ani-before-styles="{ backgroundColor: 'transparent' }"
			:ani-after-styles="{
				transform: 'translate(calc((100vw - 100rpx) / 2), calc((100vh - 100rpx) / 2)) scale(3, 3)',
				width: '100rpx',
				height: '100rpx'
			}"
			@maskClick="$refs.bigImgPopup.close()"
		>
			<image :src="imgSrc" @tap="$refs.bigImgPopup.close()" />
		</zwp-blowup-popup>

		<view class="btn" @tap="goPage('native')">去nvue页面中使用</view>
		<view class="btn" @tap="goPage('more')">动态绑定节点</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			imgSrc: 'https://dss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=2534506313,1688529724&fm=26&gp=0.jpg'
		}
	},

	methods: {
		onChange({ detail }) {
			uni.showToast({
				title: `popup${detail.value ? '显示' : '隐藏'}`,
				icon: 'none'
			})
		},
		goPage(url) {
			uni.navigateTo({
				url: `/pages/${url}/${url}`
			})
		}
	}
}
</script>

<style lang="scss" scoped>
.content {
	margin: 20px;
	width: 375rpx;
	height: 200rpx;
	line-height: 200rpx;
	text-align: center;
	font-size: 16px;
	box-shadow: 0 0 6rpx rgba(0, 0, 0, 0.3);
}

.title {
	margin: 10px 20px;
	font-size: 16px;
	color: #333;
}

image {
	width: 100rpx;
	height: 100rpx;
	border-radius: 50%;
}

.small-img {
	margin: 0 20px;
}

.btn {
	height: 40px;
	line-height: 40px;
	text-align: center;
	margin: 20px;
	border-radius: 5px;
	background-color: #00b4ff;
	color: #fff;
	font-size: 16px;
}
</style>
