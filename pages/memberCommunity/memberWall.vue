<template>
	<view>
		<view class="picker">
			<u-picker :show="showPicker" :columns="columns" @confirm="confirm" @cancel="cancel"
				@change="changeColumn"></u-picker>
			<u-button @click="showPicker = true">{{ selectedFilter }}</u-button>
			<u-button v-if="selectedFilter !== '全部'" @click="resetFilter" type="primary" size="mini"
				style="margin-left: 10rpx;">重置</u-button>
		</view>

		<view class="listShow">
			<view class="member-card" v-for="(member, index) in filteredList" :key="index">
				<image :src="member.avatar" mode="aspectFill"></image>
				<view class="member-info">
					<text class="name">{{ member.name }}</text>
					<text class="info">{{ member.branch }} | {{ member.position }}</text>
					<text class="bio" v-if="!member.showFullBio">
						{{ member.bio.substring(0, 100) }}{{ member.bio.length > 100 ? '...' : '' }}
					</text>
					<text class="bio" v-else>{{ member.bio }}</text>
					<text class="expand-btn" v-if="member.bio.length > 100"
						@click="member.showFullBio = !member.showFullBio">
						{{ member.showFullBio ? '收起' : '展开' }}
					</text>
					<!-- 技能标签 -->
					<view class="skills-container" v-if="member.skills && member.skills.length">
						<u-tag v-for="(skill, skillIndex) in member.skills" :key="skillIndex" :text="skill"
							type="primary" plain size="mini" shape="circle"
							style="margin-right: 5rpx; margin-bottom:5rpx;" />
					</view>
					<u-button type="primary" size="mini" @click="requestHelp(member)">求助</u-button>
				</view>
			</view>
		</view>
		<!-- 添加头像上传 -->
		<u-action-sheet :show="showAvatarSheet" :actions="avatarActions" title="选择头像" @close="showAvatarSheet = false"
			@select="selectAvatar"></u-action-sheet>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				showPicker: false,
				selectedFilter: '全部',
				columns: [
					['全部', '金融支部', '物联网支部', '软件支部', '电信支部', '教工支部'],
					['全部职位', '普通党员', '入党积极分子', '党支部书记', '党支部委员']
				],
				selectedColumnIndex: [0, 0],
				showAvatarSheet: false,
				avatarActions: [{
						name: '拍照'
					},
					{
						name: '从相册选择'
					},
				],

				memberList: [{
						avatar: '/static/images/头像.png', // 替换为真实头像路径
						name: '张立',
						branch: '金融支部',
						position: '普通党员',
						bio: '积极参与支部组织的各项学习活动，认真学习党的理论知识，不断提高自身政治素养。在工作中，积极发挥党员先锋模范作用，乐于助人，团结同事，多次获得“优秀员工”称号。热心参与社区志愿服务，为社区居民提供力所能及的帮助。',
						showFullBio: false, // 控制简介展开/收起
						skills: ['金融分析', '风险管理'], // 专业技能标签

					},
					{
						avatar: '/static/images/头像.png', // 替换为真实头像路径
						name: '李武',
						branch: '物联网支部',
						position: '党支部书记',
						bio: '认真履行支部书记职责，带领支部党员深入学习贯彻习近平新时代中国特色社会主义思想。积极推进支部党建工作创新，探索“智慧党建”模式，提高支部工作效率。关心支部党员的思想、工作和生活，帮助党员解决实际困难。',
						showFullBio: false,
						skills: ['物联网技术', '项目管理', '团队建设']
					},
					{
						avatar: '/static/images/头像.png', // 替换为真实头像路径
						name: '王晓梅',
						branch: '软件支部',
						position: '普通党员',
						bio: '在科研工作中，积极参与国家级科研项目，取得多项科研成果，并在核心期刊发表多篇论文。积极参与学院的教学改革，探索新的教学方法，提高教学质量。热心指导学生参加科技竞赛，并多次获得优秀指导教师奖。',
						showFullBio: false,
						skills: ['软件开发', '算法设计', '教学改革']
					},
					{
						avatar: '/static/images/头像.png', // 替换为真实头像路径
						name: '赵四',
						branch: '电信支部',
						position: '入党积极分子',
						bio: '本人积极参与社会实践，参加了多次志愿服务活动，利用所学的专业知识，为社区居民提供电子设备维修服务。',
						showFullBio: false,
						skills: ['电子设备维修', '志愿服务']
					},
					{
						avatar: '/static/images/头像.png', // 替换为真实头像路径
						name: '陈果',
						branch: '教工支部',
						position: '党支部委员',
						bio: '本人积极参与学校的各项党建工作，认真履行支部委员职责，协助支部书记做好支部日常工作。积极参与学校的“三全育人”工作，关爱学生成长，为学生提供学业指导和职业规划。',
						showFullBio: false,
						skills: ['党务工作', '学生指导', '职业规划']
					},
				],
			};
		},
		computed: {
			filteredList() {
			    if (this.selectedFilter === '全部') {
			        return this.memberList;
			    }
			
			    const filters = this.selectedFilter.split(' - ');
			    let branchFilter = null;
			    let positionFilter = null;
			
			    if (filters.length === 1) {
			        // 只有支部或只有职位
			        if (this.columns[0].includes(filters[0])) {
			            branchFilter = filters[0];
			        } else if (this.columns[1].includes(filters[0])) {
			            positionFilter = filters[0];
			        }
			    } else if (filters.length === 2) {
			        branchFilter = filters[0];
			        positionFilter = filters[1];
			    }
			
			    return this.memberList.filter(member => {
			        const branchMatch = branchFilter === null || member.branch === branchFilter;
			        const positionMatch = positionFilter === null || member.position === positionFilter;
			        return branchMatch && positionMatch;
			    });
			}
		},
		methods: {
			changeColumn(e) {
				//确保e.index存在且是一个数组
				if (e && e.index && Array.isArray(e.index) && e.index.length === this.columns.length) {
					this.selectedColumnIndex = e.index;
				}
			},
			confirm(e) {
			    const branch = e.value[0]; // 第一列选择（支部）
			    const position = e.value[1]; // 第二列选择（职位）
			
			    if (branch === '全部' && position === '全部职位') {
			        this.selectedFilter = '全部';
			    } else if (branch === '全部') {
			        this.selectedFilter = position;
			    } else if (position === '全部职位') {
			        this.selectedFilter = branch;
			    } else {
			        this.selectedFilter = `${branch} - ${position}`;
			    }
			
			    if (e && e.index && Array.isArray(e.index)) {
			        this.selectedColumnIndex = e.index;
			    }
			    this.showPicker = false;
			},
			resetFilter() {
				this.selectedFilter = "全部";
				this.selectedColumnIndex = [0, 0]
			},
			cancel() {
				this.showPicker = false; // 关闭窗口
			},
			requestHelp(member) {
				uni.navigateTo({
					url: `/pages/memberCommunity/help?helperName=${member.name}&helperBranch=${member.branch}&helperPhone=${member.phone ||
						''}`,
				});
			},
			selectAvatar(e) {
				// 处理选择头像的逻辑，例如调用相机或相册 API
				console.log('选择了：', e.name);
				this.showAvatarSheet = false;
			},
		},
	};
</script>

<style scoped>
	.picker {
		padding: 20rpx;
		background-color: #F0F9FF;
		/* 淡蓝色背景 */
	}

	.member-card {
		display: flex;
		background-color: #FFFFFF;
		/* 白色卡片 */
		padding: 20rpx;
		margin-bottom: 20rpx;
		border-radius: 10rpx;
		box-shadow: 0 2rpx 5rpx rgba(0, 0, 0, 0.1);
		/* 增加阴影 */
	}

	.member-card image {
		width: 150rpx;
		height: 150rpx;
		border-radius: 50%;
		/* 圆形头像 */
		margin-right: 20rpx;
	}

	.member-info {
		flex: 1;
		display: flex;
		/* 使用flex布局 */
		flex-direction: column;
		/* 垂直排列 */
	}

	.name {
		font-size: 32rpx;
		font-weight: bold;
		color: #1976D2;
		/* 深蓝色姓名 */
	}

	.info {
		font-size: 28rpx;
		color: #666666;
		/* 深灰色支部/职位 */
		margin-top: 10rpx;
	}

	.bio {
		font-size: 24rpx;
		color: #999999;
		/* 浅灰色简介 */
		margin-top: 15rpx;
		line-height: 1.5;
	}

	.expand-btn {
		color: #1976D2;
		/* 蓝色展开/收起按钮 */
		margin-top: 5rpx;
		font-size: 24rpx;
		text-align: right;
	}

	/* 按钮样式 */
	.u-button--primary {
		background-color: #2196F3;
		/* 蓝色按钮 */
		border-color: #2196F3;
	}

	/* 技能标签容器样式 */
	.skills-container {
		display: flex;
		flex-wrap: wrap;
		/* 允许换行 */
		margin-top: 10rpx;
	}
</style>