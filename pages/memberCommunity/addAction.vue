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
				<!-- 注意，如果需要兼容微信小程序，最好通过setRules方法设置rules规则 竞赛获奖 -->
				<u--form labelPosition="left" :model="model1" ref="form1">
					<u-form-item label="" prop="actions.name" ref="item1">
						<u--input v-model="model1.actions.name" border="surround" shape="circle"
							placeholder="联系人,只能为中文"></u--input>
					</u-form-item>
					<u-form-item label="" prop="actions.phone" borderBottom ref="item1">
						<u--input v-model="model1.actions.phone" border="surround" shape="circle"
							placeholder="请填写电话号码"></u--input>
					</u-form-item>
					<u-form-item label="" prop="actions.organization" borderBottom ref="item1">
						<u--input v-model="model1.actions.organization" border="none"
							placeholder="请填写活动组织名称"></u--input>
					</u-form-item>
					<u-form-item label="招募岗位" prop="volunteer.positon" ref="item1">
						<u--input v-model="model1.volunteer.positon" border="surround" placeholder="请填写招募岗位"></u--input>
					</u-form-item>
					<u-form-item label="招募人数" prop="volunteer.number" borderBottom ref="item1">
						<u--input v-model="model1.volunteer.number" border="none" placeholder="请填写数字"></u--input>
					</u-form-item>
					<u-form-item label="活动地点" prop="actions.area" borderBottom ref="item1">
						<u--input v-model="model1.actions.area" border="none"
							placeholder="如:广东省珠海市斗门区xxxx公园"></u--input>
					</u-form-item>
					<u-form-item label="活动简介" prop="actions.intro" ref="item1">
						<u-input v-model="model1.actions.intro" border="surround" placeholder="请填写简介" count></u-input>
					</u-form-item>
					<u-form-item label="活动内容" prop="actions.content" borderBottom ref="item1">
						<u--textarea v-model="model1.actions.content" border="none" placeholder="请填写活动内容"
							count></u--textarea>
					</u-form-item>
					<u-form-item label="活动日期" prop="actions.date" @click="showCalendar = true; hideKeyboard()"
						ref="item1">
						<u--input v-model="model1.actions.date" disabled disabledColor="#ffffff" placeholder="请选择日期"
							border="none"></u--input>
						<u-icon slot="right" name="arrow-right"></u-icon>
					</u-form-item>
					<u-form-item label="" prop="actions.starttime" @click="showTime1 = true; hideKeyboard()"
						ref="item8">
						<u--input v-model="model1.actions.starttime" disabled disabledColor="#ffffff"
							placeholder="活动开始时间" border="none"></u--input>
						<u-icon slot="right" name="arrow-right"></u-icon>
					</u-form-item>
					<u-form-item label="" prop="actions.endtime" borderBottom @click="showTime2 = true; hideKeyboard()"
						ref="item8">
						<u--input v-model="model1.actions.endtime" disabled disabledColor="#ffffff" placeholder="活动结束时间"
							border="none"></u--input>
						<u-icon slot="right" name="arrow-right"></u-icon>
					</u-form-item>
					<u-form-item label="报名限制" prop="register.limit" ref="item1">
						<u--textarea v-model="model1.register.limit" border="none" count
							placeholder="如:所有志愿者均可报名/仅限珠海学生报名"></u--textarea>
					</u-form-item>
					<u-form-item label="报名要求" prop="register.requirement" borderBottom ref="item1">
						<u--textarea v-model="model1.register.requirement" border="none" count
							placeholder="如:服从安排"></u--textarea>
					</u-form-item>
					<u-form-item label="报名截止" prop="register.deadtime" @click="registerShow = true; hideKeyboard()"
						ref="item1">
						<u--input v-model="model1.register.deadtime" disabled disabledColor="#ffffff"
							placeholder="请选择日期" border="none"></u--input>
						<u-icon slot="right" name="arrow-right"></u-icon>
					</u-form-item>
				</u--form>
				<u-button type="primary" text="提交" customStyle="margin-top: 50px" @click="submit"></u-button>
				<u-button type="error" text="重置" customStyle="margin-top: 10px" @click="reset"></u-button>
				<u-action-sheet :show="showSex" :actions="actions" title="请选择性别" description="如果选择保密会报错"
					@close="showSex = false" @select="sexSelect">
				</u-action-sheet>
				<u-calendar :show="showCalendar" mode="range" @confirm="calendarConfirm" @close="calendarClose"
					startText="开始" endText="结束" confirmDisabledText="请选择结束日期"></u-calendar>
				<u-code ref="uCode" seconds="20" @start="disabled1 = true" @end="disabled1 = false"></u-code>
				<u-datetime-picker :show="showDate" :value="birthday" mode="date" closeOnClickOverlay
					@confirm="birthdayConfirm" @cancel="birthdayClose" @close="birthdayClose"></u-datetime-picker>
				<u-datetime-picker :show="showTime1" v-model="starttime" mode="time" closeOnClickOverlay
					@confirm="startConfirm" @cancel="startCancel" @close="startClose"></u-datetime-picker>
				<u-datetime-picker :show="showTime2" v-model="endtime" mode="time" closeOnClickOverlay
					@confirm="endConfirm" @cancel="endCancel" @close="endClose"></u-datetime-picker>
				<u-datetime-picker :show="deadDateShow" v-model="deadtime" mode="datetime" closeOnClickOverlay
					@confirm="deadConfirm" @cancel="deadCancel" @change="deadChange"
					@close="deadClose"></u-datetime-picker>
				<u-datetime-picker :show="registerShow" v-model="regisTime" mode="datetime" closeOnClickOverlay
					@confirm="regisConfirm" @cancel="regisCancel" @close="regisClose"></u-datetime-picker>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				fileList1: [],
				fileList3: [{
									url: 'https://cdn.uviewui.com/uview/swiper/1.jpg',
								}],
				disabled1: false,
				showkey: false,
				deadtime: '',
				datetime: '',
				keyInput: '',
				regisTime: '',
				registerShow: false,
				deadDateShow: false,
				showTime1: false,
				showTime2: false,
				showCalendar: false,
				showDate: false,
				keyData: {
					mode: 'number',
					dotDisabled: false,
					random: false,
				},
				model1: {
					actions: {
						name: '',
						organization: '',
						phone: '',
						area: '',
						date: '',
						strattime: '',
						endtime: '',
						intro: '',
						content: ''
					},
					register: {
						limit: '',
						deadtime: '',
						requirement: ''
					},
					volunteer: {
						number: '',
						positon: ''
					},
				},
				showSex: false,
				birthday: Number(new Date()),
				starttime: '00:00',
				endtime: '00:00',
				actions: [{
						name: '男',
					},
					{
						name: '女',
					},
					{
						name: '保密',
					},
				],
				rules: {
					'actions.name': [{
						type: 'string',
						required: true,
						message: '请填写联系人',
						trigger: ['blur', 'change']
					}, {
						// 此为同步验证，可以直接返回true或者false，如果是异步验证，稍微不同，见下方说明
						validator: (rule, value, callback) => {
							// 调用uView自带的js验证规则，详见：https://www.uviewui.com/js/test.html
							return uni.$u.test.chinese(value);
						},
						message: "联系人必须为中文",
						// 触发器可以同时用blur和change，二者之间用英文逗号隔开
						trigger: ["change", "blur"],
					}],
					'actions.phone': [{
						type: 'string',
						required: true,
						message: '请填写联系方式',
						trigger: ['blur', 'change']
					}, {
						// 此为同步验证，可以直接返回true或者false，如果是异步验证，稍微不同，见下方说明
						validator: (rule, value, callback) => {
							// 调用uView自带的js验证规则，详见：https://www.uviewui.com/js/test.html
							return uni.$u.test.mobile(value);
						},
						message: "请填写正确的电话号码",
						// 触发器可以同时用blur和change，二者之间用英文逗号隔开
						trigger: ["change", "blur"],
					}],
					'volunteer.number': [{
						type: 'string',
						required: true,
						message: '请填写招募人数',
						trigger: ['blur', 'change']
					}, {
						// 此为同步验证，可以直接返回true或者false，如果是异步验证，稍微不同，见下方说明
						validator: (rule, value, callback) => {
							// 调用uView自带的js验证规则，详见：https://www.uviewui.com/js/test.html
							return uni.$u.test.digits(value);
						},
						message: "请填写整数",
						// 触发器可以同时用blur和change，二者之间用英文逗号隔开
						trigger: ["change", "blur"],
					}],
					'actions.intro': {
						type: 'string',
						min: 5,
						required: true,
						message: "不能低于5个字",
						trigger: ['blur', 'change']
					},
					'actions.area': {
						type: 'string',
						min: 10,
						required: true,
						message: '不能低于10个字',
						trigger: ['blur', 'change']
					},
					intro: {
						type: 'string',
						min: 3,
						required: true,
						message: '不低于3个字',
						trigger: ['change']
					},
					hotel: {
						type: 'string',
						min: 2,
						required: true,
						message: '请选择住店时间',
						trigger: ['change']
					},
					'userInfo.birthday': {
						type: 'string',
						required: true,
						message: '请选择生日',
						trigger: ['change']
					},
				},
				radiolist1: [{
						name: '苹果',
						disabled: false
					},
					{
						name: '香蕉',
						disabled: false
					},
					{
						name: '毒橙子',
						disabled: false
					}
				],
				checkboxList1: [{
						name: '羽毛球',
						disabled: false
					},
					{
						name: '跑步',
						disabled: false
					},
					{
						name: '爬山',
						disabled: false
					}
				]
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
			groupChange(n) {
				// console.log('groupChange', n);
			},
			radioChange(n) {
				// console.log('radioChange', n);
			},
			navigateBack() {
				uni.navigateBack()
			},
			calendarConfirm(e) {
				this.showCalendar = false
				this.model1.actions.date = `${e[0]} / ${e[e.length - 1]}`
				this.$refs.form1.validateField('hotel')
			},
			openKeyboard() {
				this.keyInput = ''
				this.show = true
			},
			calendarClose() {
				this.showCalendar = false
				this.$refs.form1.validateField('hotel')
			},
			birthdayClose() {
				this.showDate = false
				this.$refs.form1.validateField('userInfo.birthday')
			},
			birthdayConfirm(e) {
				this.showDate = false
				this.model1.userInfo.birthday = uni.$u.timeFormat(e.value, 'yyyy-mm-dd')
				this.$refs.form1.validateField('userInfo.birthday')
			},
			startClose() {
				this.showTime1 = false
			},
			startCancel() {
				this.showTime1 = false
			},
			startConfirm(e) {
				this.showTime1 = false
				this.model1.actions.starttime = e.value
				this.$refs.form1.validateField('userInfo.datetime')
			},
			endClose() {
				this.showTime2 = false
			},
			endCancel() {
				this.showTime2 = false
			},
			endConfirm(e) {
				this.showTime2 = false
				this.model1.actions.endtime = e.value
				this.$refs.form1.validateField('userInfo.datetime')
			},

			regisClose() {
				this.registerShow = false
			},
			regisCancel() {
				this.registerShow = false
			},
			regisConfirm(e) {
				this.registerShow = false
				this.model1.register.deadtime = uni.$u.timeFormat(e.value, 'yyyy-mm-dd hh:MM')
				this.$refs.form1.validateField('userInfo.datetime')
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