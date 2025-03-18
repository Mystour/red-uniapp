<template>
	<view class="container">
		<view class="u-demo-block">
			<text class="u-demo-block__title">活动图片上传：</text>
			<view class="u-demo-block__content">
				<view class="u-page__upload-item">
					<u-upload :fileList="fileList3" @afterRead="afterRead" @delete="deletePic" name="3" multiple
						:maxCount="10" :previewFullImage="true"></u-upload>
				</view>
			</view>
			<view class="u-demo-block__content">
				<u--form labelPosition="left" :model="model1" ref="form1">
				<!-- 注意，如果需要兼容微信小程序，最好通过setRules方法设置rules规则 竞赛获奖 -->
					<u-form-item label="标题" prop="prize.title" borderBottom ref="item1">
						<u--input v-model="model1.prize.title" border="none"
							placeholder="不低于5个字"></u--input>
					</u-form-item>
					<u-form-item label="竞赛类别" prop="prize.classify" borderBottom
						@click="showClassify = true; hideKeyboard()" ref="item4">
						<u--input v-model="model1.prize.classify" disabled disabledColor="#ffffff"
							placeholder="请选择类别" border="none"></u--input>
						<u-icon slot="right" name="arrow-right"></u-icon>
					</u-form-item>
					<u-form-item label="竞赛获奖" prop="prize.content" borderBottom ref="item1">
						<u--textarea v-model="model1.prize.content" height="250" maxlength="400" border="none" placeholder="竞赛获奖情况"
							count></u--textarea>
					</u-form-item>
					<u-form-item label="备注" prop="register.limit" ref="item1">
						<u--textarea v-model="model1.prize.remarks" maxlength="100" border="none" count
							placeholder=""></u--textarea>
					</u-form-item>
				</u--form>
				<u-action-sheet :show="showClassify" :actions="actions" title="请选择竞赛类别" description="如果选择其他会报错"
					@close="showClassify = false" @select="sexSelect">
				</u-action-sheet>
				<u-button type="primary" text="提交" customStyle="margin-top: 50px" @click="submit"></u-button>
				<u-button type="error" text="重置" customStyle="margin-top: 10px" @click="reset"></u-button>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				fileList1: [],
				showClassify: false,
				fileList3: [{
					url: 'https://cdn.uviewui.com/uview/swiper/1.jpg',
				}],
				model1: {
					prize: {
						title: '',
						content: '',
						remarks: '',
						classify: ''
					},
				},
				actions: [{
						name: '创新创业类',
					},
					{
						name: '学术研究类',
					},
					{
						name: '应用技能类',
					},
					{
						name: '教育普及类',
					},
					{
						name: '综合能力类',
					},
					{
						name: '其他或包含多类',
					},
				],
				rules: {
					'prize.title': {
						type: 'string',
						min: 5,
						required: true,
						message: "不能低于5个字",
						trigger: ['blur', 'change']
					},
					'prize.content': {
						type: 'string',
						min: 20,
						required: true,
						message: "不能低于20个字",
						trigger: ['blur', 'change']
					},
				},
			}
		},
		onReady() {
			// 如果需要兼容微信小程序，并且校验规则中含有方法等，只能通过setRules方法设置规则
			this.$refs.form1.setRules(this.rules)
		},
		methods: {
			afterRead(event) {
				this.fileList1.push({
					url: event.file,
					status: 'uploading',
					message: '上传中'
				})
			},
			sexSelect(e) {
				this.model1.prize.classify = e.name
				this.$refs.form1.validateField('userInfo.classify')
			},
			submit() {
				// 如果有错误，会在catch中返回报错信息数组，校验通过则在then中返回true
				this.$refs.form1.validate().then(res => {
					uni.$u.toast('校验通过')
				}).catch(errors => {
					uni.$u.toast('校验失败')
				})
			},
			reset() {
				const validateList = ['userInfo.name', 'radiovalue1', 
					'hotel', 'code', 'userInfo.birthday'
				]
				this.$refs.form1.resetFields()
				this.$refs.form1.clearValidate()
				setTimeout(() => {
					this.$refs.form1.clearValidate(validateList)
					// 或者使用 this.$refs.form1.clearValidate()
				}, 10)
			},
			hideKeyboard() {
				uni.hideKeyboard()
			},
			// 删除图片
			deletePic(event) {
				this[`fileList${event.name}`].splice(event.index, 1)
			},
			// 新增图片
			async afterRead(event) {
				// 当设置 mutiple 为 true 时, file 为数组格式，否则为对象格式
				let lists = [].concat(event.file)
				let fileListLen = this[`fileList${event.name}`].length
				lists.map((item) => {
					this[`fileList${event.name}`].push({
						...item,
						status: 'uploading',
						message: '上传中'
					})
				})
				for (let i = 0; i < lists.length; i++) {
					const result = await this.uploadFilePromise(lists[i].url)
					let item = this[`fileList${event.name}`][fileListLen]
					this[`fileList${event.name}`].splice(fileListLen, 1, Object.assign(item, {
						status: 'success',
						message: '',
						url: result
					}))
					fileListLen++
				}
			},
		},
	}
</script>

<style lang="scss" scoped>
	.container {
		margin: 30rpx;
	}
</style>