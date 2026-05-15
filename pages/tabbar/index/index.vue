<template>
  <view>
      <!-- 导航栏 -->
      <view class="box-bg">
        <uni-nav-bar statusBar="true">
          <view class="input-view">
            <uni-icons class="input-uni-icon" type="search" size="18" color="#999" />
            <input
              confirm-type="search"
              class="nav-bar-input"
              type="text"
              placeholder="输入搜索关键词"
              v-model="searchKeyword"
              @input="handleSearch"
            />
          </view>
          <template v-slot:right>
            <view class="city">搜索</view>
          </template>
        </uni-nav-bar>
      </view>

    <!-- 轮播图 -->
    <swiper indicator-active-color="#77c78c" :indicator-dots="true" :autoplay="true" interval="5000" duration="300">
      <swiper-item v-for="(image, index) in swiperImages" :key="index">
        <image class="swiper-image" :src="image" mode="aspectFill"></image>
      </swiper-item>
    </swiper>

    <!-- 汉台区标题 -->
    <text class="ht">汉台区</text>

    <!-- 景点卡片 -->
    <view v-for="(item, index) in filteredSpots" :key="index" @click="goPage(item.url)">
      <uni-card :title="item.title" isFull="true" :extra="item.extra" :thumbnail="item.thumbnail">
        <text>{{ item.description }}</text>
      </uni-card>
    </view>

    <!-- 无结果提示 -->
    <view v-if="filteredSpots.length === 0" class="no-result">
      <text>未找到相关结果</text>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      // 搜索关键词
      searchKeyword: "",
      // 轮播图图片
      swiperImages: [
        "/static/bjt1.jpg",
        "/static/lhgy1.jpg",
        "/static/xhsj1.jpg",
      ],
      // 所有景点数据
      spots: [
        { title: "兴汉胜境", description: "“兴汉胜境”旅游度假区", extra: "点击查看", thumbnail: "/static/xhsj1.jpg", url: "/pages/xhsj/xhsj" },
        { title: "石门栈道", description: "“石门栈道”旅游度假区", extra: "点击查看", thumbnail: "/static/smzd1.jpg", url: "/pages/xhsj/smzd" },
        { title: "拜将坛", description: "著名的“西汉三遗址”", extra: "点击查看", thumbnail: "/static/bjt1.jpg", url: "/pages/xhsj/bjt" },
        { title: "汉中南湖", description: "南湖风景区属于国家AAA级旅游区", extra: "点击查看", thumbnail: "/static/hznh1.jpg", url: "/pages/xhsj/hznh" },
        { title: "汉中天台国家森林公园", description: "一处自然景观与人文景观俱佳的城郊型森林公园", extra: "点击查看", thumbnail: "/static/hzttgjslgy1.jpg", url: "/pages/xhsj/hzttgjslgy" },
        { title: "汉中博物馆", description: "汉中博物馆，又称古汉台", extra: "点击查看", thumbnail: "/static/hzbwg1.jpg", url: "/pages/xhsj/hzbwg" },
        { title: "褒河森林公园", description: "山势雄伟、奇峰林立、栈道悬壁、大坝龙盘", extra: "点击查看", thumbnail: "/static/bhslgy1.jpg", url: "/pages/xhsj/bhslgy" },
        { title: "汉中民俗村", description: "国家A级旅游景区", extra: "点击查看", thumbnail: "/static/hzms1.jpg", url: "/pages/xhsj/hzmsc" },
        { title: "兴元湖公园", description: "以“帆影”为象征的水上码头", extra: "点击查看", thumbnail: "/static/xyh1.jpg", url: "/pages/xhsj/xyhgy" },
        { title: "汉中莲湖公园", description: "休息、文化、娱乐为主要功能的公园", extra: "点击查看", thumbnail: "/static/lhgy1.jpg", url: "/pages/xhsj/hzlhgy" },
        { title: "南郑区", description: "“汉家发祥地，中华聚宝盆”", extra: "点击查看", thumbnail: "/static/nzq.jpg", url: "/pages/xhsj/nzq" },
        { title: "龙头山风景区", description: "“春赏杜鹃夏避暑，秋观彩林冬滑雪”", extra: "点击查看", thumbnail: "/static/lts1.jpg", url: "/pages/xhsj/lts" },
        { title: "午子山", description: "三峰峭立，二水环流", extra: "点击查看", thumbnail: "/static/wzs1.jpg", url: "/pages/xhsj/wzs" },
        { title: "大佛洞", description: "六个岔洞，过十三趟河，登十三层石楼，闯一道鬼门关", extra: "点击查看", thumbnail: "/static/dfd1.jpg", url: "/pages/xhsj/dfd" },
      ],
      // 过滤后的景点数据
      filteredSpots: [],
    };
  },
  mounted() {
    // 初始化时显示所有景点
    this.filteredSpots = this.spots;
  },
  methods: {
    // 处理搜索输入
    handleSearch() {
      if (this.searchKeyword.trim() === "") {
        // 如果关键词为空，显示所有景点
        this.filteredSpots = this.spots;
      } else {
        // 过滤景点数据
        this.filteredSpots = this.spots.filter(
          (item) =>
            item.title.includes(this.searchKeyword) ||
            item.description.includes(this.searchKeyword)
        );
      }
    },
    // 统一跳转方法
    goPage(url) {
      uni.navigateTo({ url });
    },
  },
};
</script>

<style lang="scss">
	$nav-height: 36px; // 增加高度
	$search-bg-color: #ffffff; // 背景颜色
	$search-border-color: #e0e0e0; // 边框颜色
	$search-focus-border-color: #77c78c; // 聚焦时边框颜色
	$search-placeholder-color: #999; // 占位符颜色
	$search-text-color: #333; // 文本颜色
	
	.box-bg {
	  background-color: #F5F5F5;
	  padding: 10px 0; // 增加内边距
	}
	
	.input-view {
	  display: flex;
	  align-items: center;
	  width: 100%;
	  height: $nav-height;
	  background-color: $search-bg-color;
	  border: 1px solid $search-border-color;
	  border-radius: 20px; // 圆角
	  padding: 0 15px;
	  transition: border-color 0.3s ease; // 添加过渡效果
	
	  &:focus-within {
	    border-color: $search-focus-border-color; // 聚焦时边框颜色
	  }
	}
	
	.input-uni-icon {
	  margin-right: 10px;
	  color: $search-placeholder-color;
	}
	
	.nav-bar-input {
	  flex: 1;
	  height: 100%;
	  font-size: 14px;
	  color: $search-text-color;
	  background-color: transparent;
	  border: none;
	  outline: none;
	
	  &::placeholder {
	    color: $search-placeholder-color;
	  }
	}
	
	.city {
	  font-size: 14px;
	  color: #77c78c;
	  margin-left: 10px;
	  cursor: pointer;
	}
$nav-height: 30px;

.box-bg {
  background-color: #F5F5F5;
  padding: 5px 0;
}

.input-view {
  display: flex;
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
  padding: 0 5px;
  font-size: 12px;
  background-color: #f8f8f8;
}

.swiper-image {
  width: 100%;
  height: 300rpx;
  border-radius: 8px;
}

.ht {
  font-size: 18px;
  font-weight: bold;
  margin: 20px 0 10px 15px;
  color: #333;
}

.uni-card {
  margin: 10px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease;

  &:active {
    transform: scale(0.98);
  }
}

.no-result {
  text-align: center;
  margin-top: 20px;
  color: #777;
  font-size: 14px;
}
</style>