<template>
	<view class="party-wall-container">
		<view class="picker">
			<!-- 选择按钮样式调整 -->
			<u-button @click="showPicker = true" customStyle="background-color: #fff; color: #D81E06; border: 1px solid #D81E06;">{{ selectedFilter }}</u-button>
			<!-- 重置按钮样式调整 -->
			<u-button v-if="selectedFilter !== '全部'" @click="resetFilter" type="error" size="mini" plain style="margin-left: 10rpx;">重置</u-button>
			<u-picker :show="showPicker" :columns="columns" @confirm="confirm" @cancel="cancel"
				@change="changeColumn"></u-picker>
		</view>

		<view class="listShow">
			<view class="member-card" v-for="(member, index) in filteredList" :key="index">
				<image :src="member.avatar" mode="aspectFill" class="avatar"></image>
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
					<!-- 技能标签 - 使用 error 类型并 plain -->
					<view class="skills-container" v-if="member.skills && member.skills.length">
						<u-tag v-for="(skill, skillIndex) in member.skills" :key="skillIndex" :text="skill"
							type="error" plain size="mini" shape="circle"
							style="margin-right: 5rpx; margin-bottom:5rpx;" />
					</view>
                    <!-- 求助按钮样式调整 -->
					<u-button type="error" size="mini" @click="requestHelp(member)" class="help-button">求助</u-button>
				</view>
			</view>
		</view>
		<!-- 添加头像上传 -->
		<u-action-sheet :show="showAvatarSheet" :actions="avatarActions" title="选择头像" @close="showAvatarSheet = false"
			@select="selectAvatar"></u-action-sheet>

	</view>
</template>

<script>
	// <script> 部分保持不变
	export default {
	    data() {
	        return {
	            showPicker: false,
	            selectedFilter: '全部',
	            columns: [
	                ['全部', '金融支部', '物联网支部', '软件支部', '电信支部', '教工支部'],
	                ['全部职位', '普通党员', '预备党员', '党支部书记', '党支部委员'] // 添加了'预备党员'选项
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

	            memberList: [
	                {
	                    avatar: '/static/images/avatar_liuzixuan.png', // 替换为实际头像路径
	                    name: '刘子轩',
	                    branch: '物联网支部',
	                    position: '普通党员', // PDF中转正
	                    bio: '获北京工业大学学习优秀奖、都柏林学院学习单项奖、“青创北京”2023年“挑战杯”首都大学生课外学术科技作品竞赛“青学二十大”红色专项赛三等奖。',
	                    showFullBio: false,
	                    skills: ['物联网技术', '学习能力强', '挑战杯竞赛'],
	                },
	                {
	                    avatar: '/static/images/avatar_raohanshu.jpg', // 替换为实际头像路径
	                    name: '饶瀚书',
	                    branch: '软件支部',
	                    position: '普通党员', // PDF中转正
	                    bio: '获北京工业大学学习优秀奖。研究生推免至华东师范大学。',
	                    showFullBio: false,
	                    skills: ['软件开发', '学习优秀', '推免上岸'],
	                },
	                {
	                    avatar: '/static/images/avatar_yangwenya.jpg', // 替换为实际头像路径
	                    name: '杨雯雅',
	                    branch: '软件支部',
	                    position: '普通党员', // PDF中转正
	                    bio: '获都柏林学院学习优秀奖。研究生推免至天津大学。',
	                    showFullBio: false,
	                    skills: ['学习优秀', '软件工程', '推免上岸'],
	                },
	                {
	                    avatar: '/static/images/avatar_zhangyouke.jpg', // 替换为实际头像路径
	                    name: '张有恪',
	                    branch: '软件支部',
	                    position: '普通党员', // PDF中转正
	                    bio: '获都柏林学院学习进步奖。',
	                    showFullBio: false,
	                    skills: ['学习进步', '软件工程', '潜力股'],
	                },
	                {
	                    avatar: '/static/images/avatar_yangziqi.jpg', // 替换为实际头像路径
	                    name: '杨子棋',
	                    branch: '软件支部',
	                    position: '普通党员', // PDF中转正
	                    bio: '获美国大学生数学建模比赛M奖, IEEE 极限编程比赛国际二等奖等。研究生推免至中国科学院网络信息中心。',
	                    showFullBio: false,
	                    skills: ['数学建模', '算法编程', 'IEEE竞赛', '推免上岸'],
	                },
	                 {
	                    avatar: '/static/images/avatar_yuzeying.jpg', // 替换为实际头像路径
	                    name: '于泽瀛',
	                    branch: '软件支部',
	                    position: '普通党员', // PDF中转正
	                    bio: '获“青创北京”2022年“挑战杯”首都大学创业计划竞赛省级银奖,“互联网+”大学生创新创业大赛北京赛区二等奖。',
	                    showFullBio: false,
	                    skills: ['创新创业', '挑战杯竞赛', '互联网+大赛'],
	                },
	                 {
	                    avatar: '/static/images/avatar_guoyunfei.jpg', // 替换为实际头像路径
	                    name: '郭芸菲',
	                    branch: '金融支部',
	                    position: '普通党员', // PDF中转正
	                    bio: '获北京工业大学三好学生奖, 北京工业大学三力先锋。研究生推免至清华大学(直博)。',
	                    showFullBio: false,
	                    skills: ['三好学生', '三力先锋', '金融学霸', '直博清华'],
	                },
	                {
	                    avatar: '/static/images/avatar_zhaojiaqi.jpg', // 替换为实际头像路径
	                    name: '赵佳棋',
	                    branch: '金融支部',
	                    position: '普通党员', // PDF中转正
	                    bio: '获北京工业大学三好学生奖。',
	                    showFullBio: false,
	                    skills: ['三好学生', '金融学'],
	                },
	                {
	                    avatar: '/static/images/avatar_zouxinyu.jpg', // 替换为实际头像路径
	                    name: '邹欣语',
	                    branch: '金融支部',
	                    position: '普通党员', // PDF中转正
	                    bio: '获北京工业大学学习优秀奖。',
	                    showFullBio: false,
	                    skills: ['学习优秀', '金融学'],
	                },
	                {
	                    avatar: '/static/images/avatar_ouyangzhimei.jpg', // 替换为实际头像路径
	                    name: '欧阳智美',
	                    branch: '金融支部',
	                    position: '普通党员', // PDF中转正
	                    bio: '获北京工业大学学习优秀奖。研究生推免至中南大学。',
	                    showFullBio: false,
	                    skills: ['学习优秀', '金融学', '推免上岸'],
	                },
	                 {
	                    avatar: '/static/images/avatar_liruoxi.jpg', // 替换为实际头像路径
	                    name: '李若兮',
	                    branch: '金融支部',
	                    position: '普通党员', // PDF中转正
	                    bio: '获第七届全国学术英语词汇竞赛三等奖。',
	                    showFullBio: false,
	                    skills: ['英语词汇竞赛', '金融学', '英语能力强'],
	                },
	                {
	                    avatar: '/static/images/avatar_zhangkairui.png', // 替换为实际头像路径
	                    name: '张凯睿',
	                    branch: '电信支部', // 映射自 电子信息工程
	                    position: '普通党员', // PDF中转正
	                    bio: '获北京工业大学学习优秀奖。研究生推免至北京邮电大学。',
	                    showFullBio: false,
	                    skills: ['学习优秀', '电子信息工程', '推免上岸'],
	                },
	                {
	                    avatar: '/static/images/avatar_liuziqi.jpg', // 替换为实际头像路径
	                    name: '柳子祺',
	                    branch: '电信支部', // 映射自 电子信息工程
	                    position: '普通党员', // PDF中转正
	                    bio: '获北京工业大学学习优秀奖。研究生推免至北京理工大学。',
	                    showFullBio: false,
	                    skills: ['学习优秀', '电子信息工程', '推免上岸'],
	                },
	                {
	                    avatar: '/static/images/avatar_zhaiyanqiao.jpg', // 替换为实际头像路径
	                    name: '翟彦乔',
	                    branch: '电信支部', // 映射自 电子信息工程
	                    position: '普通党员', // PDF中转正
	                    bio: '获都柏林学院学习优秀奖。研究生推免至西安电子科技大学。',
	                    showFullBio: false,
	                    skills: ['学习优秀', '电子信息工程', '推免上岸'],
	                },
	                 {
	                    avatar: '/static/images/头像.png', // PDF中无头像，使用占位符
	                    name: '郑泽幸',
	                    branch: '软件支部',
	                    position: '预备党员', // PDF P12
	                    bio: '积极向党组织靠拢，努力学习党的理论知识，不断提升思想觉悟。', // 补充通用描述
	                    showFullBio: false,
	                    skills: ['积极分子', '软件工程'], // 补充通用技能
	                },
	                 {
	                    avatar: '/static/images/头像.png', // PDF中无头像，使用占位符
	                    name: '陈子昂',
	                    branch: '软件支部',
	                    position: '预备党员', // PDF P12
	                    bio: '认真学习党的路线方针政策，积极参加支部活动，向优秀党员看齐。',// 补充通用描述
	                    showFullBio: false,
	                    skills: ['积极分子', '软件工程'],// 补充通用技能
	                },
	                  {
	                    avatar: '/static/images/头像.png', // PDF中无头像，使用占位符
	                    name: '陈丹盈',
	                    branch: '金融支部',
	                    position: '预备党员', // PDF P12
	                    bio: '思想上积极进步，努力学习专业知识，乐于助人，团结同学。',// 补充通用描述
	                    showFullBio: false,
	                    skills: ['积极分子', '金融学'],// 补充通用技能
	                },
	                  {
	                    avatar: '/static/images/头像.png', // PDF中无头像，使用占位符
	                    name: '刘心怡',
	                    branch: '金融支部',
	                    position: '预备党员', // PDF P12
	                    bio: '积极向党组织递交入党申请书，主动汇报思想动态，接受党组织的考验。',// 补充通用描述
	                    showFullBio: false,
	                    skills: ['积极分子', '金融学'],// 补充通用技能
	                },
	            ],
	        };
	    },
	    computed: {
	        filteredList() {
	            const branchIndex = this.selectedColumnIndex[0];
	            const positionIndex = this.selectedColumnIndex[1];

	            // 添加防御性检查，确保 selectedColumnIndex 和 columns 结构正确
	            if (!this.columns || this.columns.length < 2 || !this.columns[0] || !this.columns[1] ||
	                branchIndex === undefined || positionIndex === undefined ||
	                branchIndex >= this.columns[0].length || positionIndex >= this.columns[1].length) {
	                console.warn("筛选条件或数据结构异常，返回原始列表");
	                return this.memberList;
	            }


	            const branchFilter = this.columns[0][branchIndex];
	            const positionFilter = this.columns[1][positionIndex];

	            return this.memberList.filter(member => {
	                const branchMatch = branchFilter === '全部' || member.branch === branchFilter;
	                const positionMatch = positionFilter === '全部职位' || member.position === positionFilter;
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
	            // 添加检查，确保 e.value 和 e.index 存在且为数组
	             if (!e || !e.value || !Array.isArray(e.value) || e.value.length !== this.columns.length ||
	                 !e.index || !Array.isArray(e.index) || e.index.length !== this.columns.length) {
	                 console.error("确认事件参数错误", e);
	                 this.showPicker = false; // 仍然关闭窗口
	                 return; // 提前返回，避免后续错误
	             }

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

	            this.selectedColumnIndex = e.index;
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
    /* 整体容器背景 */
    .party-wall-container {
        background-color: #F5F5F5; /* 浅灰色背景 */
        min-height: 100vh; /* 确保至少占满屏幕 */
    }

	.picker {
		padding: 20rpx;
		background-color: #FDE2E2; /* 淡红色背景 */
        border-bottom: 1px solid #f0f0f0; /* 添加分隔线 */
        display: flex; /* 让按钮横向排列 */
        align-items: center; /* 垂直居中 */
	}

    /* 选择按钮自定义样式 */
    .picker >>> .u-button { /* 可能需要使用深度选择器 >>> */
        /* background-color: #fff !important;
        color: #D81E06 !important;
        border: 1px solid #D81E06 !important; */
        margin-right: 10rpx; /* 增加按钮间距 */
    }

    /* 重置按钮 */
    .picker >>> .u-button--error.is-plain { /* 确保能选中 plain 状态的 error 按钮 */
        color: #D81E06 !important;
        border-color: #D81E06 !important;
        background-color: #fef0f0 !important; /* uview plain error 的背景色 */
    }

	.member-card {
		display: flex;
		background-color: #FFFFFF; /* 白色卡片 */
		padding: 30rpx; /* 增加内边距 */
		margin: 20rpx; /* 调整外边距 */
		border-radius: 16rpx; /* 更圆润的边角 */
		box-shadow: 0 4rpx 12rpx rgba(0, 0, 0, 0.08); /* 稍微调整阴影 */
        border: 1px solid #FCE2E2; /* 添加非常淡的红色边框 */
	}

	.avatar { /* 给头像添加class，方便样式控制 */
		width: 120rpx; /* 稍微缩小头像 */
		height: 120rpx;
		border-radius: 50%;
		margin-right: 30rpx; /* 增加与右侧信息的间距 */
        border: 2px solid #eee; /* 给头像加个灰色边框 */
	}

	.member-info {
		flex: 1;
		display: flex;
		flex-direction: column;
	}

	.name {
		font-size: 34rpx; /* 增大姓名 */
		font-weight: bold;
		color: #D81E06; /* 党建红 */
	}

	.info {
		font-size: 26rpx; /* 缩小一点 */
		color: #666666;
		margin-top: 8rpx; /* 调整间距 */
	}

	.bio {
		font-size: 26rpx; /* 增大一点简介 */
		color: #888888; /* 稍微加深简介颜色 */
		margin-top: 20rpx;
		line-height: 1.6; /* 增加行高 */
	}

	.expand-btn {
		color: #E53935; /* 使用稍浅一点的红色 */
		margin-top: 10rpx;
		font-size: 24rpx;
		text-align: right;
		align-self: flex-end; /* 确保按钮在右侧 */
	}

	/* 技能标签容器样式 */
	.skills-container {
		display: flex;
		flex-wrap: wrap;
		margin-top: 15rpx; /* 调整间距 */
        margin-bottom: 15rpx; /* 增加与求助按钮的间距 */
	}

    /* u-tag 已经在 template 中通过 type="error" plain 设置了党建风格 */

    /* 求助按钮 */
    .help-button {
       align-self: flex-end; /* 按钮靠右 */
       margin-top: auto; /* 将按钮推到底部（如果希望的话） */
       /* 如果 uview 的 type="error" 颜色不符合，可以自定义 */
       /* background-color: #D81E06 !important;
       border-color: #D81E06 !important; */
       /* color: #fff !important; */
       /* padding: 4rpx 16rpx !important; */ /* 微调按钮大小 */
    }
</style>