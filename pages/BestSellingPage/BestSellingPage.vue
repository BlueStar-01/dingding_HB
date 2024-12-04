<template>
  <view class="table">
    <view class="table-row" v-for="(item, index) in tableData" :key="index">
      <!-- 图片区域 -->
      <view class="image-area">
        <image :src="item.imageUrl" mode="aspectFill" class="image"></image>
      </view>
      <!-- 文本区域 -->
      <view class="text-area">
        <text class="title">{{ item.title }}</text>
        <text class="description">{{ item.description }}</text>
      </view>

      <!-- 价格区域 -->
      <view class="price-area">
        <text class="current-price">{{ item.currentPrice }}元</text>
        <text class="original-price">{{ item.originalPrice }}元</text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        {
          imageUrl: "https://s3proxy.cdn-zlib.sk/covers150/collections/userbooks/ca9f14c0560ed0acb624a98dab85d87569cd4ecde98fd2369cf39265ef2f12e3.jpg",
          title: '恋人不行 1',
          description: '「我再也不要孤零零的了！我要赢得最棒的高中生活！」舍弃孤零零的中学时代，在高中初次亮相的我——甘织玲奈子。\n 但我本性阴暗，没办法习惯我所憧憬的阳光生活，要窒息了！就在这时，因为一些意外我与我们学校的超级巨星·王冢真唯成为了共享彼此烦恼的密友。\n只要有真唯在，我每天都能努力——本应如此！',
          currentPrice: '199',
          originalPrice: '299',
        },
        {
          imageUrl: 'https://s3proxy.cdn-zlib.sk/covers150/collections/userbooks/ef1e929a1bf14e5832da1ea87e48e1240c734703a611a3e85b778baca54d0f26.jpg',
          title: '恋人不行 2',
          description: '「我再也不要孤零零的了！我要赢得最棒的高中生活！」舍弃孤零零的中学时代，在高中初次亮相的我——甘织玲奈子。\n 但我本性阴暗，没办法习惯我所憧憬的阳光生活，要窒息了！就在这时，因为一些意外我与我们学校的超级巨星·王冢真唯成为了共享彼此烦恼的密友。\n只要有真唯在，我每天都能努力——本应如此！',
          currentPrice: '199',
          originalPrice: '299',
        },
      ]
    }
  }
}
</script>

<style scoped>
.table {
  margin-top: 20px;
  padding: 10px;
}

.table-row {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  border-bottom: 1px solid #ccc;
  padding: 10px 0;
  position: relative; /* 使价格区域可以相对定位于表格项 */
}

.image-area {
  width: 150px;
  height: 220px;
  margin-right: 20px;
}

.image {
  width: 100%;
  height: 100%;
  border-radius: 8px;
}

.text-area {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center; /* 使标题居中 */
  text-align: center;  /* 让标题文本也居中显示 */
}

.title {
  font-size: 16px;
  font-weight: bold;
  margin-bottom: 5px;
}

.description {
  font-size: 14px;
  color: #888;
}

.price-area {
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  position: absolute; /* 使价格区域定位到表格项的右下角 */
  bottom: 10px;
  right: 10px;
}

.current-price {
  font-size: 16px;
  font-weight: bold;
  color: #e60012;
  margin-right: 10px;
}

.original-price {
  font-size: 14px;
  color: #888;
  text-decoration: line-through;
  position: relative;
}


</style>
