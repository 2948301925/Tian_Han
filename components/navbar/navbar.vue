<template>
	<view>
		<uni-section title="自定义内容" subTitle="使用 left/right/default 插槽自定义内容" type="line" style="margin-bottom: 3px;">
			<view class="box-bg">
				<uni-nav-bar statusBar="true"> 
					<view class="input-view">
						<uni-icons class="input-uni-icon" type="search" size="18" color="#999" />
						<input confirm-type="search" class="nav-bar-input" type="text" placeholder="输入搜索关键词">
					</view>
					<template v-slot:right>
						<view class="city">
							搜索
						</view>
					</template>
				</uni-nav-bar>
			</view>
		</uni-section>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

 <style lang="scss">
   	$nav-height: 30px;
   
   	.box-bg {
   		background-color: #F5F5F5;
   		padding: 5px 0;
   	}
   
   	.input-view {
   		/* #ifndef APP-PLUS-NVUE */
   		display: flex;
   		/* #endif */
   		flex-direction: row;
   		width: 600rpx;
   		flex: 1;
   		background-color: #f8f8f8;
   		height: $nav-height;
   		border-radius: 15px;
   		padding: 0 15px;
   		flex-wrap: nowrap;
   		margin: 7px 0;
   		line-height: $nav-height;
   	}
   
   	.input-uni-icon {
   		line-height: $nav-height;
   	}
   
   	.nav-bar-input {
   		height: $nav-height;
   		line-height: $nav-height;
   		/* #ifdef APP-PLUS-NVUE */
   		width: 670rpx;
   		/* #endif */
   		padding: 0 5px;
   		font-size: 12px;
   		background-color: #f8f8f8;
   	}
</style>
