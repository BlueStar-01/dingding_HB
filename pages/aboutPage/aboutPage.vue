<template>
  <view class="container">
    <!-- 页面标题 -->
    <view class="page-title">
      <text class="title">公司详情</text>
    </view>

    <!-- 关于我们简介 -->
    <view class="section">
      <text class="section-title">公司简介</text>
      <text class="section-content">
        我们是一个致力于推动科技创新的公司，专注于提供创新型产品和解决方案。我们的使命是通过科技改变生活，让每一个人都能体验到科技带来的便利与进步。
      </text>
    </view>

    <!-- 使命与愿景 -->
    <view class="section">
      <text class="section-title">我们的使命与愿景</text>
      <text class="section-content">
        使命：通过技术创新与优质服务，提供世界级的产品体验，为用户创造更多的价值。
        <br /><br />
        愿景：成为全球领先的科技公司，推动科技进步和社会可持续发展。
      </text>
    </view>

    <!-- 团队成员 -->
    <view class="section">
      <text class="section-title">我们的团队</text>
      <view class="team-members">
        <view class="team-member" v-for="(member, index) in teamMembers" :key="index">
          <img :src="member.image" class="team-member-image" />
		  <br />
          <text class="team-member-name">{{ member.name }}</text>
          <text class="team-member-role">{{ member.role }}</text>
        </view>
      </view>
    </view>

    <!-- 联系我们 -->
    <view class="section contact">
      <text class="section-title">联系我们</text>
      <text class="contact-info">邮箱：contact@company.com</text>
      <text class="contact-info">电话：+123 456 7890</text>
      <text class="contact-info">地址：某某路某某大厦</text>
    </view>

    <!-- 页脚 -->
    <footer>
      <a href="#" id="copyright">© 2024 公司名称</a>
    </footer>
  </view>
</template>

<script>
export default {
  data() {
    return {
      teamMembers: [
        {
          name: "甘织玲奈子",
          role: "屑粉毛",
          image: "https://img.moegirl.org.cn/common/f/fa/Wata-nare_chara01_trans.png"
        },
        {
          name: "王冢真唯",
          role: "大小姐",
          image: "https://img.moegirl.org.cn/common/d/d9/Wata-nare_chara02_trans.png"
        },
        {
          name: "濑名紫阳花",
          role: "天使",
          image: "https://img.moegirl.org.cn/common/6/6e/Wata-nare_chara03_trans.png"
        }
      ]
    };
  }
};
</script>

<style scoped>
/* 页面整体样式 */
.container {
  padding: 20px;
  background-color: #f9f9f9;
  box-sizing: border-box;
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
}

.page-title {
  text-align: center;
  margin-bottom: 30px;
}

.title {
  font-size: 32px;
  font-weight: bold;
  color: #333;
}

/* 区域样式 */
.section {
  margin-bottom: 30px;
}

.section-title {
  font-size: 22px;
  font-weight: bold;
  color: #007bff;
  margin-bottom: 10px;
}

.section-content {
  font-size: 16px;
  color: #555;
  line-height: 1.6;
}

/* 团队成员样式 */
.team-members {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.team-member {
  width: 30%;
  text-align: center;
}

.team-member-image {
  width: ;
  height: 180px;
  object-fit: cover;
  border-radius: 8px;
  margin-bottom: 10px;
}

.team-member-name {
  font-size: 18px;
  font-weight: bold;
  color: #333;
}

.team-member-role {
  font-size: 14px;
  color: #888;
}

/* 联系方式样式 */
.contact {
  background-color: #fff;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.contact-info {
  font-size: 16px;
  color: #555;
  margin-bottom: 10px;
}

/* 页脚样式 */
footer {
  background-color: #333;
  padding: 20px;
  text-align: center;
  color: white;
}

#copyright {
  color: white;
  text-decoration: none;
}

#copyright:hover {
  color: #007bff;
}
</style>
