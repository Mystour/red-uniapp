<template>
	<view class="container">
		<u--form labelPosition="left" :model="model" :rules="rules" ref="uForm">
			<text>您的问题或建议：</text>
			<u-form-item label="" prop="userInfo.name" ref="item1" class="u-demo-block__content" borderBottom>
				<u--textarea class="textarea" v-model="model.suggestion" placeholder="请输入内容" count></u--textarea>
			</u-form-item>
			<view class="contact">
				<text>您的联系方式：</text>
				<u-form-item label="" prop="userInfo.phone" ref="item1">
					<u--input placeholder="电话号码" border="surround" v-model="model.userInfo.phone"
						@change="change"></u--input>
				</u-form-item>
				<u-form-item label="" prop="userInfo.email" ref="item1">
					<u--input placeholder="电子邮箱" border="surround" v-model="model.userInfo.email"
						@change="change"></u--input>
				</u-form-item>
				<u-button text="提交" size="normal" shape="circle" type="error" style="width: 650rpx;margin-top: 60rpx;"></u-button>
			</view>
		</u--form>
	</view>
</template>

<script>
	export default {
		components: {},
		data() {
			return {
				model: {
					userInfo: {
						phone: '',
						email: '',
					},
					suggestion: '',
				},
				rules: {
					'userInfo.phone': [{
						// 	type: 'string',
						// 	required: true,
						// 	message: '请填写手机号',
						// 	trigger: ['blur', 'change']
						// }, {
						// 此为同步验证，可以直接返回true或者false，如果是异步验证，稍微不同，见下方说明
						validator: (rule, value, callback) => {
							if (!value) {
								return
							}
							// 调用uView自带的js验证规则，详见：https://www.uviewui.com/js/test.html
							return uni.$u.test.mobile(value);
						},
						message: "请填写正确手机号",
						// 触发器可以同时用blur和change，二者之间用英文逗号隔开
						trigger: ["change", "blur"],
					}],
					'userInfo.email': [{
						// 	type: 'string',
						// 	required: true,
						// 	message: '请填写手机号',
						// 	trigger: ['blur', 'change']
						// }, {
						// 此为同步验证，可以直接返回true或者false，如果是异步验证，稍微不同，见下方说明
						validator: (rule, value, callback) => {
							// 调用uView自带的js验证规则，详见：https://www.uviewui.com/js/test.html
							return uni.$u.test.email(value);
						},
						message: "请填写正确邮箱",
						// 触发器可以同时用blur和change，二者之间用英文逗号隔开
						trigger: ["change", "blur"],
					}],
				}
			};
		},
		methods: {
			change(e) {
				// console.log(e);
			},
		}
	};
</script>

<style scoped>
	.u-demo-block__content {
		width: 700rpx;
	}

	.container {
		padding: 30rpx 20rpx;
	}

	.contact {
		margin: 30rpx 0;
	}
</style>