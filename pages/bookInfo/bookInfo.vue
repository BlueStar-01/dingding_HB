<template>
  <view class="container">
    <view class="book-info" v-if="book">
      <!-- 书籍封面图片，如果book.coverImg不存在，则使用默认图片 -->
      <image :src="book.coverImg || defaultCoverUrl" class="cover-img" mode="aspectFill"></image>
      
      <!-- 书籍详细信息 -->
      <view class="info-wrapper">
        <text class="title">{{ book.name }}</text>
        <view class="detail-row">
          <text class="detail-label">作者:</text>
          <text class="detail-value">{{ book.author }}</text>
        </view>
        <view class="detail-row">
          <text class="detail-label">出版社:</text>
          <text class="detail-value">{{ book.publishing }}</text>
        </view>
        <view class="detail-row">
          <text class="detail-label">ISBN:</text>
          <text class="detail-value">{{ book.isbn }}</text>
        </view>
        <view class="detail-row">
          <text class="detail-label">价格:</text>
          <text class="detail-value">{{ book.price }} 元</text>
        </view>
        <view class="detail-row" v-if="book.description">
          <text class="detail-label">描述:</text>
          <text class="detail-value">{{ book.description }}</text>
        </view>
      </view>
    </view>
    <view v-else>
      <text>加载中...</text>
    </view>
  </view>
</template>

<script>
import { ref, computed } from 'vue';
import { baseURL } from '../../common/PublicValues';

export default {
  data() {
    return {
      bookId: null, // 从路由参数中获取的书籍ID
      book: null, // 存储从服务器获取的书籍信息
    };
  },
  computed: {
    // 计算属性，用于定义默认书籍封面图片的URL
    defaultCoverUrl() {
      // 这里应该返回您的默认封面图片的URL
      return 'https://example.com/default-cover.jpg'; // 请替换为实际的URL
    },
  },
  onLoad(options) {
    this.bookId = options.bookId;
    console.log(options);
    this.loadBook(this.bookId);
  },
  methods: {
    async loadBook(id) {
      try {
        const response = await uni.request({
          url: `${baseURL}/book`,
          method: 'GET',
          data: {
            bookID: id,
          },
          header: {
            'Content-Type': 'application/json',
          },
          success: (res) => {
            if (res.statusCode === 200 && res.data && res.data.code === 1) {
              this.book = res.data.data;
            } else {
              console.error('获取书籍信息失败', res.data.msg || '未知错误');
              uni.showToast({
                title: `发生错误：${res.data.msg || '未知错误'}`,
                duration: 2000,
              });
            }
          },
          fail: (err) => {
            console.error('网络请求失败', err);
          },
        });
      } catch (error) {
        console.error('请求过程中发生异常', error);
      }
    },
  },
};
</script>

<style scoped>
.container {
  padding: 20px;
}

.book-info{
	
}

.cover-img {
  width: 262.5rpx; /* 调整封面图片宽度 */
  object-fit: cover;
  float: left; /* 让封面图片浮动到左边 */
  margin-right: 20px; /* 在图片和详细信息之间添加间距 */
}

.info-wrapper {
  overflow: hidden; /* 确保详细信息不会溢出到封面图片下方 */
}

.title {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 15px;
}

.detail-row {
  margin-bottom: 10px;
}

.detail-label {
  font-weight: bold;
  display: inline-block;
  width: 70px; /* 调整标签宽度以匹配您的布局 */
}

.detail-value {
  display: inline-block;
}
</style>