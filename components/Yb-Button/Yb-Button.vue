<template>
	<button hover-class='none' :disabled="isDisabled" :class="{
		'yb-button': true, 
		[getSizeClassName()]: getSizeClassName(),
		[getTypeClassName()]: getTypeClassName(),
		'is-round': round,
		'yb-button-disabled': isDisabled
		}"
		v-on="$listeners">
		<view class=" iconfont icon-Loading yb-button-loading"
	 v-if="loading"></view>
	<slot></slot>
	</button>
</template>

<script>
	export default {
		parentMsg: function(msg) {
			this.messages.push(msg)
		},
		props: {
			/*
				type: 主要：primary，信息：info，成功：success，危险: danger，警告：warning
			*/
			type: String,
			// size: small, large
			size: String,
			// 圆角
			round: Boolean,
			// 是否为加载状态
			loading: Boolean,
			disabled: Boolean
		},
		computed: {
			isDisabled() {
				return this.loading || this.disabled;
			}
		},
		methods: {
			getSizeClassName() {
				const SIZE = {
					small: 'yb-button-small',
					large: 'yb-button-large',
				}
				console.log(SIZE[this.size]);
				return SIZE[this.size] || 'yb-button-default';
			},
			getTypeClassName() {
				const TYPES = {
					primary: 'yb-button-primary',
					success: 'yb-button-success',
					danger: 'yb-button-danger',
					info: 'yb-button-info',
					warning: 'yb-button-warning'
				}
				return TYPES[this.type] || ''
			},
		}
	}
</script>

<style lang="scss">
	// 颜色
	$color-primary: #e33e33;
	$color-success: #67c23a;
	$color-info: #909399;
	$color-warning: #e6a23c;
	$color-danger: rgb(196, 76, 85);
	.yb-button::after {
		  border: none;
		}
	.yb-button {
		display: flex;
		justify-content: center;
		align-items: center;
		border: 1upx solid #aaa;
		background-color: #fff;
		min-width: 130upx;
		width: max-content;
		background-color: #f8f8f8;
		border-radius: 30upx;
		font-size: 30upx;
		height: 70upx;
		padding: 0 25upx;
		border-radius: 10upx;
		.yb-button-loading {
			font-size: inherit;
		}
	}

	.yb-button:active {
		opacity: .7;
	}
	
	.yb-button.yb-button-default {
		.yb-button-loading {
			margin-right: 8upx;
		}
	}

	.is-round.yb-button-default {
		border-radius: 35upx;
	}

	// 小号按钮
	.yb-button.yb-button-small {
		min-width: 100upx;
		height: 48upx;
		font-size: 22upx;
		border-radius: 8upx;
		padding: 0 20upx;
		.yb-button-loading {
			margin-right: 5upx;
		}
	}

	.is-round.yb-button-small {
		border-radius: 25upx;
	}

	// 大号按钮
	.yb-button.yb-button-large {
		min-width: 700upx;
		height: 100upx;
		font-size: 45upx;
		border-radius: 13upx;
		padding: 0 40upx;
		.yb-button-loading {
			margin-right: 15upx;
		}
	}

	.is-round.yb-button-large {
		border-radius: 75upx;
	}


	// 按钮颜色
	.yb-button.yb-button-primary {
		background-color: $color-primary;
		color: #fff;
		border: none;
	}

	.yb-button.yb-button-success {
		background-color: $color-success;
		color: #fff;
		border: none;
	}

	.yb-button.yb-button-info {
		background-color: $color-info;
		color: #fff;
		border: none;
	}

	.yb-button.yb-button-danger {
		background-color: $color-danger;
		color: #fff;
		border: none;
	}

	.yb-button.yb-button-warning {
		background-color: $color-warning;
		color: #fff;
		border: none;
	}

	// loading
	.yb-button-loading {
		margin: 3upx;
		font-size: inherit;
		animation: rotate 2s linear infinite;
	}
	// 禁用
	.yb-button.yb-button-disabled {
		opacity: .7;
	}
	
	@keyframes rotate {
		0% {
			transform: rotateZ(0)
		}
		0% {
			transform: rotateZ(360deg)
		}
	}

	// 字体图标
	@font-face {
		font-family: "iconfont";
		src: url('//at.alicdn.com/t/font_1987587_049u6oe93a0c.eot?t=1596597427124');
		/* IE9 */
		src: url('//at.alicdn.com/t/font_1987587_049u6oe93a0c.eot?t=1596597427124#iefix') format('embedded-opentype'),
			/* IE6-IE8 */
			url('data:application/x-font-woff2;charset=utf-8;base64,d09GMgABAAAAAAMQAAsAAAAABzAAAALBAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHEIGVgCCcAqCOIIWATYCJAMICwYABCAFhG0HMRs9BsiemjwpEkKCgAzb2zAGQoiH//b73z4z82zuF0+qyageVesjUUmEAglKge7tS6MEQrFMZN3LqapzH6/uQm0nkYv2QBmLebwcecknK4t1EtCg7kFoC2ALWP/vpuiN2ZgYadF+nsCd/g+UBRbIDYaKBsrnuRzfXXkYzu8Nt7U2LZo0LOvFAQW0N0aRXSAFxg1jNxE4hMcEqkWKjmub+znUrwCrAvGSOQbqz9mUlsrQF7o1B4t4r6Of3qZvyDv++fiLRD9JJwM1t19s2Gj5FyicD9oDz/MB+XweWMfI2IcU4n6t76YumdvXpQa5bqvQviqDX9qWynb7xyOILlA+AuZV2T3JseJWf5lAQR9DyKtRafqjI4AYvez1dSDOTjDzaJ/OjxBc/+AhN+iHocV6NnjNjnVzV0p3OzVu1zJyy1p88gm6+/eu/4AX80Qci/OHj2Dy8vlUD6p+gd77/5AcUJIol/R0I637VZKuE71UDiOr0wdvF925FqgsDkqp2nd+PUHmx2a5nLBpIKWyTvSxmU9/foJlCO15hoblH/8d3998zzk2/6+/KeDnjS8eac8L6hdA+rfnD36zvGdHCZXAnoovry0lQ/23X1dVtPTQlL+xptl38oR+Tm4h6VlA1rdOFOY+OhpH6Oq7iGrP1vHGNKFLlAF2nSoIE96QjDlDNuGHKMxfdMz5R9dEdKF6GFMXNjaDDa4JMCTY2GxhZvGQIqccFJUZcGq+IbJKzimAiFkSp7VUsbgFIYg5tsR1h0hJMRU8wJvKc+D7HEeCu2BJrSplNJtM0ro3aRYP0KCrBGCQgA0ztWCMhQtROlwaLNGfARw1PoNoaRtIFgAhxsbH0jSpHsSWLuzVdi+vxOochCRRGCVwAWxTmQd8Pg6L6ue5gEXSVEdkIrOSsBftq9PWNwRfdwQqYE4BZ2a969ywWeggBAAAAA==') format('woff2'),
			url('//at.alicdn.com/t/font_1987587_049u6oe93a0c.woff?t=1596597427124') format('woff'),
			url('//at.alicdn.com/t/font_1987587_049u6oe93a0c.ttf?t=1596597427124') format('truetype'),
			/* chrome, firefox, opera, Safari, Android, iOS 4.2+ */
			url('//at.alicdn.com/t/font_1987587_049u6oe93a0c.svg?t=1596597427124#iconfont') format('svg');
		/* iOS 4.1- */
	}

	.iconfont {
		font-family: "iconfont" !important;
		font-size: 16px;
		font-style: normal;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
	}

	.icon-Loading:before {
		content: "\e834";
	}
</style>
