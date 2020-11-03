## 类似手机app打开动画的popup（从app的位置开始，由小变大）
___
### 示例代码
```html
<template>
	<view>
		<view id="normal" class="content" @tap="$refs.popup.open()">点击显示放大popup</view>
		<zwp-blowup-popup ref="popup" selector="normal">
			<!-- 这个是占位用的空文本组件 -->
			<placeholder-text :pNum="2" :lNum="5" />
			<view class="btn" @tap="$refs.popup.close()">点击隐藏</view>
		</zwp-blowup-popup>
	</view>
</template>

<style scoped>
	.content {
		margin: 20px;
		width: 375rpx;
		height: 200rpx;
		line-height: 200rpx;
		text-align: center;
		font-size: 16px;
		box-shadow: 0 0 6rpx rgba(0, 0, 0, 0.3);
	}
</style>
```
### ** 注意事项 **
1. 关于`everyTimeQuery`属性：如果绑定的元素位置乱动（包括页面的滚动使元素发生位移），或者是动态绑定元素，就设置为true；位置大小完全不会变的元素默认false就可以了
2. 关于`maskStyles`属性：使用下面代码说明
   ```js
	{
		position: 'fixed',
		bottom: 0,
		top: 0,
		left: 0,
		right: 0,
		backgroundColor: 'rgba(0, 0, 0, 0.3)',
		zIndex: 998,
		...this.maskStyles
		// 如果maskStyles里有重名的属性则会覆盖默认样式
	}
	```
3. 关于`aniBeforeStyles`和`aniAfterStyles`属性：假设`aniBeforeStyles`中设置了背景色为红色，`aniAfterStyles`中设置背景色为黑色，展示的结果是：popup刚出现时为红色，随着放大渐渐过渡到黑色
4. 关于`duration`属性：显示popup时是透明度和放大同时进行，隐藏popup时是先缩小然后变透明，`duration`只影响放大缩小的时间，透明度的过渡时间固定为300ms
5. 关于`timingFn`属性：同上，只影响放大缩小的速度曲线，透明度固定为ease-in-out

### 使用说明

| 名称        | 类型   |  默认值  | 描述 |
| --------   | -----:  | :----:  | :----:  |
| selector | String   |   -  |绑定元素的id，必填|
| everyTimeQuery  |  Boolean  |  false |是否每次显示都重新获取节点信息|
| maskStyles| Object |  {} |为蒙层添加样式|
| aniBeforeStyles | Object |  {} |为弹出层的内容部分添加样式|
| aniAfterStyles | Object |  {}  |为弹出层的内容部分添加样式，在显示之后、放大之前添加到元素上|
| duration | Number |  300  |单位ms，popup过渡动画时间|
| timingFn | String |  ease-in-out  |popup过渡动画速度曲线|

### 插槽说明

| 名称        | 描述   |
| --------   | :----:  | 
| default   | popup中的内容  |
`示例代码`
```html
<zwp-blowup-popup ref="popup" selector="normal">
	<text>这里是popup中展示的内容</text>
</zwp-blowup-popup>
```

### 事件
| 名称        | 描述   | 返回值 |
| --------   | -----:  | -----:  | 
| @change | 当popup显示/隐藏时触发，注意，是动画结束之后才触发的，event.detail = { value }  | - |
| @maskClick | 点击蒙层触发事件  | - |
