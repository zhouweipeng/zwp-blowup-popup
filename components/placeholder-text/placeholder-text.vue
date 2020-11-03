<template>
	<view>
		<view v-for="ITEM in pNum" :key="`p${ITEM}`">
			<view v-for="(item, index) in lNum" :key="`l${ITEM}${item}`" :class="['empty-text', !index ? 'empty-text-start' : index == lNum - 1 ? 'empty-text-end' : '']" />
		</view>
	</view>
</template>

<script>
export default {
	props: {
		// 段落数
		pNum: {
			type: Number,
			default: 2
		},
		// 行数 （因为每一段的第一行和最后一行的样式和中间行不一样，所以行数最少2行）
		lNum: {
			type: Number,
			default: 3
		}
	}
}
</script>

<style scoped>
.empty-text {
	height: 25px;
	margin: 10px;
	background-color: #f5f5f5;
}

.empty-text-start {
	transform-origin: right center;
	transform: scaleX(0.9);
}

.empty-text-end {
	transform-origin: left center;
	transform: scaleX(0.5);
	margin-bottom: 20px;
}
</style>
