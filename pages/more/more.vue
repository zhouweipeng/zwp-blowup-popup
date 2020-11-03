<template>
	<view class="more-page">
		<view v-for="(item, index) in list" :key="index" :id="`content${index}`" class="content-item" @tap="showPopup(true, index)">第{{ index + 1 }}条</view>
		<zwp-blowup-popup
			ref="popup"
			:selector="contentId"
			every-time-query
			:ani-before-styles="{ borderRadius: '20px', lineHeight: '40px' }"
			:ani-after-styles="{ borderRadius: '0' }"
		>
			<view class="popup-title">这里是第{{ currContentIndex + 1 }}条的内容</view>
			<placeholder-text :pNum="2" :lNum="5" />
			<view class="btn" @tap="showPopup(false)">点击收回</view>
		</zwp-blowup-popup>
	</view>
</template>

<script>
export default {
	data() {
		return {
			list: new Array(5).fill(),
			currContentIndex: null
		}
	},

	computed: {
		contentId() {
			return 'content' + this.currContentIndex
		}
	},

	methods: {
		showPopup(flag, index) {
			this.currContentIndex = flag ? index : null
			this.$nextTick(this.$refs.popup[flag ? 'open' : 'close'])
		}
	}
}
</script>

<style lang="scss" scoped>
.more-page {
	overflow: hidden;

	.content-item {
		height: 40px;
		line-height: 40px;
		text-align: center;
		font-size: 16px;
		margin: 20px;
		box-shadow: 0 0 6rpx rgba(0, 0, 0, 0.3);
		border-radius: 20px;
	}
	
	.popup-title {
		text-align: center;
		font-size: 16px;
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
}
</style>
