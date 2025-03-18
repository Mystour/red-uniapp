<template>
  <view class="content">
    <view class="u-demo-block">
      <text class="u-demo-block__title">请填写求助信息</text>
      <view class="u-demo-block__content">
        <u--form labelPosition="left" :model="formData" ref="form" :rules="rules">
          <u-form-item label="求助类别" prop="helpType" borderBottom>
            <u--input v-model="formData.helpType" disabled placeholder="请选择求助类别" @click.native="showTypePicker = true"></u--input>
            <u-icon slot="right" name="arrow-right" @click="showTypePicker = true"></u-icon>
          </u-form-item>
          <u-form-item label="紧急程度" prop="urgency" borderBottom  v-if="formData.helpType">
            <u--input v-model="formData.urgency" disabled placeholder="请选择紧急程度（可选）" @click.native="showUrgencyPicker = true"></u--input>
            <u-icon slot="right" name="arrow-right" @click="showUrgencyPicker = true"></u-icon>
          </u-form-item>
          <u-form-item label="被求助人" prop="helperName" borderBottom>
            <u--input v-model="formData.helperName" :disabled="!!formData.helperName"
              placeholder="请填写被求助人姓名"></u--input>
          </u-form-item>
          <u-form-item label="被求助人支部" prop="helperBranch" borderBottom>
            <u--input v-model="formData.helperBranch" :disabled="!!formData.helperBranch"
              placeholder="请填写被求助人支部"></u--input>
          </u-form-item>
          <u-form-item label="情况概述" prop="description" borderBottom>
            <u--textarea v-model="formData.description" placeholder="请详细描述您遇到的问题和需要的帮助" maxlength="500"
              :count="true"></u--textarea>
            <!-- 可选：语音输入 -->
            <!-- <u-button type="primary" size="mini" @click="startVoiceInput">语音输入</u-button> -->
          </u-form-item>
          <u-form-item>
            <u-button type="primary" @click="submitForm">提交</u-button>
          </u-form-item>

        </u--form>

        <u-action-sheet :show="showTypePicker" :actions="helpTypes" title="选择求助类别" @close="showTypePicker = false"
          @select="selectHelpType"></u-action-sheet>
        <u-action-sheet :show="showUrgencyPicker" :actions="urgencyLevels" title="选择紧急程度"
          @close="showUrgencyPicker = false" @select="selectUrgency"></u-action-sheet>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        helpType: '',
        urgency: '',
        helperName: '', // 被求助人姓名
        helperBranch: '',
        helperPhone: '', // 被求助人电话（可选）
        description: '',
      },
      showTypePicker: false,
      showUrgencyPicker: false,
      helpTypes: [{
          name: '学业辅导'
        },
        {
          name: '就业咨询'
        },
        {
          name: '生活困难'
        },
        {
          name: '心理咨询'
        },
        {
          name: '技术难题'
        },
        {
          name: '其他'
        },
      ],
      urgencyLevels: [{
          name: '一般'
        },
        {
          name: '紧急'
        },
        {
          name: '非常紧急'
        },
      ],
      rules: {
        helpType: [{
          required: true,
          message: '请选择求助类别',
          trigger: 'change'
        }],
        description: [{
          required: true,
          message: '请填写情况概述',
          trigger: 'blur'
        }],
      },
    };
  },
  onLoad(options) {
    // 从党员墙页面获取参数
    if (options.helperName) {
      this.formData.helperName = options.helperName;
      this.formData.helperBranch = options.helperBranch
    }
  },
  onReady() {
    this.$refs.form.setRules(this.rules);
  },
  methods: {
    selectHelpType(item) {
      this.formData.helpType = item.name;
      this.showTypePicker = false;
      this.$refs.form.validateField('helpType');
    },
    selectUrgency(item) {
      this.formData.urgency = item.name;
      this.showUrgencyPicker = false;
       this.$refs.form.validateField('urgency');
    },
    submitForm() {
      this.$refs.form.validate(valid => {
        if (valid) {
          // 提交表单数据到后端
          console.log('提交数据:', this.formData);

          // 模拟提交成功
          uni.showToast({
            title: '提交成功',
            icon: 'success',
            duration: 2000,
            complete: () => {
              // 发送通知（消息推送或短信） - 需后端配合
              this.sendNotification();

              // 跳转到成功提示页或返回党员墙
              // uni.navigateTo({ url: '/pages/success' });
              uni.navigateBack();
            },
          });
        }
      });
    },
    sendNotification() {
      // 模拟发送通知（实际应用中需要后端接口支持）
      console.log('发送通知给求助者和被求助者...');
      // ...
    },
    // startVoiceInput() {
    //   // 调用语音输入API（如科大讯飞、百度语音等）
    //   // ...
    // },
  },
};
</script>