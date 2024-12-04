<template>
  <view class="container">
    <!-- 页面标题 -->
    <view class="page-title">
      <text class="title">提交反馈</text>
    </view>

    <!-- 说明区域 -->
    <view class="description">
      <text class="desc-text">欢迎来到我们的“联系我们”页面！如果您有任何问题、意见或建议，请填写下面的表单。我们将尽快与您取得联系！</text>
    </view>

    <!-- 联系表单 -->
    <form @submit="handleSubmit">
      <view class="form-group">
        <text class="label">姓名</text>
        <input
          v-model="formData.name"
          class="input-field"
          placeholder="请输入您的姓名"
          type="text"
          required
        />
      </view>

      <view class="form-group">
        <text class="label">邮箱</text>
        <input
          v-model="formData.email"
          class="input-field"
          placeholder="请输入您的邮箱"
          type="email"
          required
        />
      </view>

      <view class="form-group">
        <text class="label">留言内容</text>
        <textarea
          v-model="formData.message"
          class="textarea-field"
          placeholder="请输入您的留言"
          required
        ></textarea>
      </view>

      <!-- 提交按钮 -->
      <button class="submit-btn" type="submit">提交</button>
    </form>

    <!-- 提交后的反馈信息 -->
    <view v-if="submitStatus" class="submit-feedback">
      <text>{{ submitStatus }}</text>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        name: '',
        email: '',
        message: ''
      },
      submitStatus: '', // 提交状态信息
    };
  },
  methods: {
    // 提交表单
    handleSubmit(event) {
      event.preventDefault(); // 阻止表单默认提交行为

      // 简单的表单验证
      if (!this.formData.name || !this.formData.email || !this.formData.message) {
        this.submitStatus = '所有字段都是必填项，请完整填写！';
        return;
      }

      // 模拟表单提交（实际应用中你会通过 API 提交到服务器）
      setTimeout(() => {
        this.submitStatus = '感谢您的留言，我们会尽快联系您！';
        // 清空表单
        this.formData = { name: '', email: '', message: '' };
      }, 1000); // 模拟网络请求延迟
    }
  }
};
</script>

<style scoped>
/* 页面布局样式 */
.container {
  padding: 20px;
  background-color: #f9f9f9;
  box-sizing: border-box; /* 确保padding不影响元素宽度 */
  width: 100%;
  max-width: 600px; /* 限制容器的最大宽度 */
  margin: 0 auto; /* 页面居中 */
}

/* 页面标题样式 */
.page-title {
  text-align: center;
  margin-bottom: 20px;
}

.title {
  font-size: 26px;
  font-weight: bold;
  color: #333;
}

/* 说明区域样式 */
.description {
  background-color: #fff;
  padding: 15px;
  margin-bottom: 30px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.desc-text {
  font-size: 16px;
  color: #555;
  line-height: 1.6;
  text-align: center;
}

/* 表单样式 */
.form-group {
  margin-bottom: 20px;
}

.label {
  font-size: 16px;
  color: #333;
  margin-bottom: 5px;
  display: block;
}

.input-field,
.textarea-field {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 16px;
  background-color: white;
  box-sizing: border-box; /* 防止溢出边界 */
}

.textarea-field {
  height: 150px;
  resize: none;
}

/* 提交按钮 */
.submit-btn {
  background-color: #007bff;
  color: white;
  padding: 14px 20px;
  font-size: 18px;
  width: 100%;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-btn:hover {
  background-color: #0056b3;
}

.submit-btn:active {
  background-color: #004085;
}

/* 提交反馈信息 */
.submit-feedback {
  margin-top: 20px;
  text-align: center;
  color: #28a745;
  font-size: 16px;
}
</style>
