<template>
	<view class="container">
		<!-- 书籍推荐区域 -->
		<view class="recommend">
			<view class="recommend-item" v-for="(book, index) in books" :key="index">
				<div class="recommend-info">
					<text class="book-title">{{ book.name }}</text>
					<br />
					<img :src="book.coverImg" alt="书籍" class="recommend-image" />
					<button class="btn" @click="goToBookInfo(book.id)">查看详细内容</button>
					<button class=" btn" @click="addCart(book)">加入购物车</button>
				</div>
			</view>
		</view>

		<!-- 分页按钮（横向） -->
		<view class="pagination">
			<!-- <button 
        class="page-btn" 
        v-if="currentPage > 1" 
        @click="goToPage(1)">
        1
      </button> -->

			<button class="page-btn" v-if="currentPage > 1" @click="goToPage(currentPage - 1)">
				上一页
			</button>

			<!-- 显示分页按钮 -->
			<button v-for="page in totalPages" :key="page" class="page-btn" :class="{'active': page === currentPage}"
				@click="goToPage(page)">
				{{ page }}
			</button>

			<button class="page-btn" v-if="currentPage < totalPages" @click="goToPage(currentPage + 1)">
				下一页
			</button>

			<!-- <button 
        class="page-btn" 
        v-if="currentPage < totalPages" 
        @click="goToPage(totalPages)">
        {{ totalPages }}
      </button> -->
		</view>
	</view>
</template>

<script>
	import {
		baseURL
	} from '../../common/PublicValues.js';

	export default {
		mounted() {
			console.log(baseURL); // 访问全局变量
			this.fetchBooks(); // 页面加载时获取书籍数据
		},
		data() {
			return {
				books: [],
				currentPage: 1,
				totalPages: 0,
				pageSize: 10,
			};
		},
		methods: {
			async fetchBooks() {
				try {
					const response = await uni.request({
						url: `${baseURL}/book/page`,
						method: 'GET',
						data: {
							pageNo: this.currentPage,
							pageSize: this.pageSize,
						},
						header: {
							'Content-Type': 'application/json',
						},
					});

					if (response.statusCode === 200 && response.data && response.data.code === 1) {
						const {
							records,
							total,
							pages
						} = response.data.data;
						this.books = records;
						this.totalPages = pages;
					} else {
						console.error('获取书籍数据失败', response);
					}
				} catch (error) {
					console.error('请求失败', error);
				}
			},
			goToPage(page) {
				if (page >= 1 && page <= this.totalPages) {
					this.currentPage = page;
					this.fetchBooks();
				}
			},
			goToBookInfo(bookId) {
				uni.navigateTo({
					url: `/pages/bookInfo/bookInfo?bookId=${bookId}`,
					success: () => console.log("跳转成功"),
					fail: () => console.error("跳转失败"),
				});
			},
			async addCart(book) {
				try {
					const response = await uni.request({
						url: `${baseURL}/cart`,
						method: 'PUT',
						data: {
							book.id,
							book.coverImg,
							Add: 1,
						},
						header: {
							'Content-Type': 'application/json',
						},
					});

					if (response.statusCode === 200 && response.data && response.data.code === 1) {
						uni.showToast({
							title: '添加成功',
							icon: 'success',
							duration: 2000,
						});
					} else {
						uni.showToast({
							title: '添加书籍到购物车失败',
							icon: 'error',
							duration: 2000,
						});
					}
				} catch (error) {
					uni.showToast({
						title: '发生未知错误',
						icon: 'error',
						duration: 2000,
					});
					console.error('请求失败', error);
				}
			},
		},
	};
</script>

<style scoped>
	/* 页面整体样式 */
	.container {
		padding: 20px;
		background-color: #f5f5f5;
		max-width: 1200px;
		/* 限制最大宽度 */
		margin: 0 auto;
		/* 居中 */
	}

	/* 页面标题 */
	.page-title {
		text-align: center;
		margin-bottom: 20px;
	}

	.title {
		font-size: 28px;
		font-weight: bold;
		color: #333;
	}

	/* 书籍推荐区域 */
	.recommend {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
		/* 每列最小250px */
		gap: 20px;
		border: 2px solid #e0e0e0;
		border-radius: 8px;
		padding: 10px;
		background-color: white;
	}

	.recommend-item {
		border: 1px solid #ddd;
		border-radius: 8px;
		background-color: white;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
		overflow: hidden;
		padding: 10px;
		transition: transform 0.3s ease-in-out;
	}

	.recommend-item:hover {
		transform: translateY(-5px);
	}

	/* 调整图片显示方式 */
	.recommend-image {
		height: 220px;
		/* 固定高度为220px */
		object-fit: cover;
		/* 保持比例，裁剪多余部分 */
		border-bottom: 2px solid #f0f0f0;
	}

	.recommend-info {
		padding: 10px;
		text-align: center;
	}

	.book-title {
		font-size: 16px;
		font-weight: bold;
		color: #333;
		margin-bottom: 10px;
	}

	.btn {
		background-color: #007bff;
		color: white;
		border: none;
		padding: 8px 12px;
		margin: 5px 0;
		border-radius: 5px;
		cursor: pointer;
		transition: background-color 0.3s ease;
		font-size: 14px;
	}

	.btn:hover {
		background-color: #0056b3;
	}

	.btn:active {
		background-color: #004085;
	}

	/* 分页样式 */
	.pagination {
		display: flex;
		justify-content: center;
		align-items: center;
		margin-top: 20px;
		gap: 8px;
		/* 控制按钮之间的间距 */
	}

	.page-btn {
		background-color: #007bff;
		color: white;
		border: none;
		padding: 8px 12px;
		margin: 0 5px;
		border-radius: 5px;
		cursor: pointer;
		transition: background-color 0.3s ease;
		font-size: 14px;
	}

	.page-btn:disabled {
		background-color: #cccccc;
		cursor: not-allowed;
	}

	.page-btn:hover {
		background-color: #0056b3;
	}

	.page-btn.active {
		background-color: #0056b3;
		font-weight: bold;
	}

	.page-info {
		font-size: 16px;
		font-weight: bold;
		color: #333;
	}

	/* 响应式设计：对小屏设备进行调整 */
	@media (max-width: 768px) {
		.recommend {
			grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
			/* 在小屏设备上减少每行的书籍数量 */
		}

		.page-btn {
			font-size: 12px;
			/* 调小分页按钮的字体 */
			padding: 6px 10px;
			/* 调整分页按钮大小 */
		}
	}

	@media (max-width: 480px) {
		.title {
			font-size: 22px;
			/* 标题字体调整 */
		}

		.recommend {
			grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
			/* 更窄的显示 */
		}

		.page-btn {
			font-size: 10px;
			/* 分页按钮字体更小 */
			padding: 5px 8px;
			/* 调整分页按钮大小 */
		}
	}
</style>