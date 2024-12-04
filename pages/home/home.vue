<template>
	<view class="container">
		<view id="nav" class="nav">
			<view class="logo">钉钉书屋</view>
			<navigator class="nav-link" url="/pages/home/home">首页</navigator>
			<navigator class="nav-link" url="/pages/NewBooksPage/NewBooksPage">书库</navigator>
			<navigator class="nav-link" url="/pages/BestSellingPage/BestSellingPage">特价促销</navigator>
			<navigator class="nav-link" url="/pages/PromotionsPage/PromotionsPage">联系我们</navigator>
			<navigator class="nav-link" url="/pages/aboutPage/aboutPage">关于我们</navigator>
		</view>

		<!-- 页面内容 -->
		<view class="home-content">
			<uni-swiper-dot :info="info" :current="current" field="content" :mode="mode">
				<swiper class="swiper-box" @change="change">
					<swiper-item v-for="(item ,index) in info" :key="index">
						<view class="swiper-item">
							<image class="banner-image" :src="item.url" mode="widthFix" />
						</view>
					</swiper-item>
				</swiper>
			</uni-swiper-dot>
			<!-- <view class="banner">
				<image class="banner-image" src="https://img.moegirl.org.cn/common/4/4c/Watanare_bg_01.jpeg"
					mode="widthFix" />
			</view> -->

			<!-- 热门推荐 -->
			<view class="section">
				<text class="section-title">热门推荐</text>
				<view class="book-list">
					<view class="book-item" v-for="(book, index) in recommendedBooks" :key="index"
						@mouseenter="hoveredIndex = index" @mouseleave="hoveredIndex = null">
						<view class="book-cover-wrapper">
							<!-- 书籍封面 -->
							<image :src="book.imgUrl" mode="widthFix" class="book-cover" :alt="book.title" />
							<!-- 书籍简介 -->
							<view class="book-description" v-show="hoveredIndex === index">
								<text class="book-title">{{ book.title }}</text>
								<br />
								<text class="book-summary">{{ book.summary }}</text>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>

		<!-- 页脚 -->
		<footer>
			<view class="content">
				<text>{{ currentDateTime }}</text>
			</view>
			<a href="#" id="copyright">© 2024 钉钉书屋</a>
		</footer>
	</view>
</template>

<script>
	export default {
		name: 'HomePage',
		data() {
			return {
				currentDateTime: '',
				info: [{
						colorClass: 'uni-bg-red',
						url: 'https://bluestar-web-start.oss-cn-hangzhou.aliyuncs.com/Snipaste_2024-11-13_21-11-11.png',
						content: '内容 A'
					},
					{
						colorClass: 'uni-bg-green',
						url: 'https://bluestar-web-start.oss-cn-hangzhou.aliyuncs.com/Snipaste_2024-11-07_23-11-25.png',
						content: '内容 B'
					},
					{
						colorClass: 'uni-bg-blue',
						url: 'https://bluestar-web-start.oss-cn-hangzhou.aliyuncs.com/%E3%82%B8%E3%83%A3%E3%82%B1%E3%83%83%E3%83%88%E3%82%A4%E3%83%A9%E3%82%B9%E3%83%88%EF%BC%88%E6%96%87%E5%AD%97%E3%81%AA%E3%81%97%EF%BC%89.jpg',
						content: '内容 C'
					}
				],
				hoveredIndex: null, // 用来标识当前悬停的书籍索引
				recommendedBooks: [{
						title: "书籍1",
						imgUrl: "https://s3proxy.cdn-zlib.sk/covers400/collections/userbooks/746bca3caaf0e1c5ddd27d17f18a046d8d04fcbb8cb4413b30b7bdabec14cd02.jpg",
						summary: "这本书讲述了一个关于勇气与冒险的故事。"
					},
					{
						title: "书籍2",
						imgUrl: "https://s3proxy.cdn-zlib.sk/covers400/collections/userbooks/746bca3caaf0e1c5ddd27d17f18a046d8d04fcbb8cb4413b30b7bdabec14cd02.jpg",
						summary: "这本书是科幻小说，探索了未来的科技世界。"
					},
					{
						title: "书籍3",
						imgUrl: "https://s3proxy.cdn-zlib.sk/covers400/collections/userbooks/746bca3caaf0e1c5ddd27d17f18a046d8d04fcbb8cb4413b30b7bdabec14cd02.jpg",
						summary: "一本经典的爱情小说，讲述了跨越时间与空间的爱情。"
					},
					{
						title: "书籍4",
						imgUrl: "https://s3proxy.cdn-zlib.sk/covers400/collections/userbooks/746bca3caaf0e1c5ddd27d17f18a046d8d04fcbb8cb4413b30b7bdabec14cd02.jpg",
						summary: "这本书深入探讨了哲学的本质，适合思考人生的人。"
					}
				]
			};
		},
		methods: {
			change() {

			},
			getCurrentDateTime() {
				const now = new Date();
				const year = now.getFullYear();
				const month = String(now.getMonth() + 1).padStart(2, '0'); // 月份从0开始，需要加1
				const day = String(now.getDate()).padStart(2, '0');
				const hours = String(now.getHours()).padStart(2, '0');
				const minutes = String(now.getMinutes()).padStart(2, '0');
				const seconds = String(now.getSeconds()).padStart(2, '0');

				this.currentDateTime = `${year}-${month}-${day} ${hours}:${minutes}:${seconds}`;
			}

		},
		mounted() {
			this.getCurrentDateTime();
			// 每秒更新一次时间（可选）
			setInterval(this.getCurrentDateTime, 1000);
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

	#nav {
		background-color: #333;
		padding: 10px 15px;
		/* 导航栏内边距增加 */
		color: white;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.logo {
		font-size: 20px;
		font-weight: bold;
		color: white;
	}

	.nav-link {
		color: white;
		margin-left: 20px;
		text-decoration: none;
		font-size: 16px;
	}

	.nav-link:hover {
		color: #007bff;
	}

	.home-content {
		padding: 20px 0;
		margin-top: 20px;
	}

	/* Banner */
	.swiper-box {
		height: 200px;
	}

	.swiper-item {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 200px;
		color: #fff;
	}

	/* 热门推荐 */
	.section {
		margin-bottom: 30px;
	}

	.section-title {
		font-size: 22px;
		font-weight: bold;
		color: #007bff;
		margin-bottom: 10px;
	}

	.book-list {
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		/* 使书籍项均匀分布 */
		gap: 15px;
	}

	.book-item {
		width: 45%;
		/* 控制每个书籍项占用的宽度 */
		text-align: center;
		background-color: white;
		border-radius: 8px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
		padding: 10px;
		margin-bottom: 15px;
		/* 给每个书籍项添加底部间距 */
		position: relative;
		overflow: hidden;
		cursor: pointer;
	}

	.book-cover-wrapper {
		position: relative;
	}

	.book-cover {
		width: 100%;
		height: 220px;
		object-fit: cover;
		border-radius: 6px;
		transition: transform 0.3s ease, opacity 0.3s ease;
	}

	.book-item:hover .book-cover {
		transform: rotateY(180deg);
		/* 旋转封面 */
		opacity: 0;
		/* 隐藏封面 */
	}

	/* 书籍简介 */
	.book-description {
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		padding: 10px;
		background-color: rgba(255, 255, 255, 0.8);
		border-radius: 8px;
		opacity: 0;
		visibility: hidden;
		transition: opacity 0.3s ease, visibility 0.3s ease;
	}

	.book-item:hover .book-description {
		opacity: 1;
		visibility: visible;
	}

	.book-title {
		font-size: 16px;
		font-weight: bold;
		color: #333;
	}

	.book-summary {
		font-size: 14px;
		color: #666;
		margin-top: 10px;
	}

	/* 页脚样式 */
	footer {
		background-color: #333;
		padding: 20px 15px;
		text-align: center;
		color: white;
		margin-top: 30px;
	}

	#copyright {
		color: white;
		text-decoration: none;
	}

	#copyright:hover {
		color: #007bff;
	}
</style>