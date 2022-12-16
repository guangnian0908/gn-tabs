<template>
	<view class="gn-tabs" :class="[ceiling?'ceilSty':'']">
		<view class="tab-box" :style="{'justify-content':justify}">
			<view class="tab-item" v-for="(item,index) in tabList" :key="index" @click="TabClick(index)"
				:class="tabIndex == item.id?'active':''">
				<image :src="item.image" v-if='showImage' mode=""></image>
				<text :style="{'font-size': fontSize+'rpx','color': fontColor}">{{item.name}}</text>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		props: {
			tabIndexNow: { //默认选中
				type: Number,
				default: 0
			},
			tabList: { //传入数据
				type: Array,
				default: []
			},
			justify: { //展示方式
				type: String,
				default: 'space-around'
			},
			showImage: { //是否显示图片(暂不可用)
				type: Boolean,
				default: false
			},
			fontSize: { //字体大小
				type: Number,
				default: 30
			},
			ceiling: { //吸顶(暂不可用)
				type: Boolean,
				default: false
			},
			fontColor: { //字体颜色
				type: String,
				default: '#262626'
			},
		},
		data() {
			return {
				tabIndex: 0,
			}
		},
		created() {
			this.tabIndex = this.tabIndexNow
		},
		methods: {
			TabClick(index) {
				this.$emit('change', index)
				this.tabIndex = index
			}
		}
	}
</script>
<style lang="scss" scoped>
	.gn-tabs {
		height: 70rpx;
		padding-top: 30rpx;
		background-color: white;
		border-bottom: 1rpx solid #cfcfcf;
	}

	.ceilSty {
		// 设置定位效果为“吸顶”
		position: sticky;
		// 吸顶的“位置”
		top: 0;
		// 提高层级，防止被轮播图覆盖
		z-index: 999;
	}

	.tab-box {
		max-width: 750rpx;
		height: 50rpx;
		display: flex;

		.tab-item {
			width: 150rpx;
			flex-shrink: 0;
			position: relative;
			transition: all 0.2s linear;
			font-weight: 500;
			text-align: center;
			color: #262626;

			image {
				display: block;
				width: 100rpx;
				height: 100rpx;
				margin: 20rpx;
			}

			&::after {
				transition: all 0.2s linear;
				transform: translateX(-50%) scaleX(0);
				content: '';
				width: 50%;
				position: absolute;
				left: 50%;
				bottom: 0;
				border-bottom: 6rpx solid #00aaff;
				border-radius: 26rpx;
			}

			&.active {
				&::after {
					font-weight: 500;
					content: '';
					width: 50%;
					font-weight: bold;
					position: absolute;
					left: 50%;
					bottom: 0;
					transform: translateX(-50%) scaleX(1);
					border-bottom: 6rpx solid #00aaff;
					border-radius: 26rpx;
				}
			}
		}
	}
</style>
