<template>
  <view class="map-container">
    <!-- 地图组件 -->
    <map
      id="map"
      :latitude="latitude"
      :longitude="longitude"
      :markers="markers"
      :scale="scale"
      :show-location="true"
      style="width: 100%; height: 100vh;"
    >
    </map>

    <!-- 返回按钮 -->
    <view class="back-button" @click="goBack">
      <uni-icons type="arrowleft" size="24" color="#333" />
    </view>

    <!-- 定位按钮 -->
    <view class="center-button" @click="centerMap">
      <uni-icons type="location-filled" size="24" color="#77c78c" />
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      latitude: 0, // 纬度
      longitude: 0, // 经度
      scale: 16, // 地图缩放级别
      markers: [], // 地图标记
      mapContext: null, // 地图上下文对象
    };
  },
  onLoad() {
    // 获取用户当前位置
    this.getUserLocation();

    // 获取地图上下文对象
    this.mapContext = uni.createMapContext("map", this);
  },
  methods: {
    // 获取用户当前位置
    getUserLocation() {
      uni.getLocation({
        type: "wgs84", // 坐标系类型
        success: (res) => {
          this.latitude = res.latitude;
          this.longitude = res.longitude;

          // 添加当前位置标记
          this.markers = [
            {
              id: 1,
              latitude: res.latitude,
              longitude: res.longitude,
              name: "我的位置",
              iconPath: "/static/location.png", // 指针图标
              width: 30,
              height: 30,
            },
          ];
        },
        fail: (err) => {
          console.error("获取位置失败：", err);
          uni.showToast({
            title: "获取位置失败，请检查权限",
            icon: "none",
          });
        },
      });
    },

    // 返回上一页
    goBack() {
      uni.navigateBack();
    },

    // 将地图中心点移动到用户当前位置
    centerMap() {
      if (this.mapContext) {
        this.mapContext.moveToLocation({
          latitude: this.latitude,
          longitude: this.longitude,
        });
      }
    },
  },
};
</script>

<style lang="scss">
.map-container {
  position: relative;
  width: 100%;
  height: 100vh;
}

.back-button {
  position: absolute;
  top: 20px;
  left: 20px;
  width: 40px;
  height: 40px;
  background-color: #fff;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  z-index: 999;
}

.center-button {
  position: absolute;
  top: 20px;
  right: 20px;
  width: 40px;
  height: 40px;
  background-color: #fff;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  z-index: 999;
}
</style>