<template>
  <view class="personal-container">
    <view class="user-info">
      <view class="avatar-box">
        <input v-if="isEditAvatar" type="file" @change="selectAvatar">
        <image v-else class="avatar" :src="avatarSrc"></image>
      </view>
      <view class="username-box">
        <input v-if="isEdit" class="username" v-model="userName" placeholder="请输入用户名">
        <text v-else class="username">{{userName}}</text>
      </view>
    </view>
    <view class="function-buttons">
      <view class="function-item" @click="toggleEditAvatar">
        {{isEditAvatar? '保存头像' : '修改用户头像'}}
      </view>
      <view class="function-item" @click="toggleEdit">
        {{isEdit? '保存用户名' : '修改用户名'}}
      </view>
    </view>
  </view>
</template>
<script>
export default {
  data() {
    return {
      userName: '用户名',
      isEdit: false,
      avatarSrc: '你的头像路径',
      isEditAvatar: false
    }
  },
  methods: {
    toggleEdit() {
      this.isEdit =!this.isEdit;
    },
    toggleEditAvatar() {
      this.isEditAvatar =!this.isEditAvatar;
    },
    selectAvatar(e) {
      const file = e.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (event) => {
          this.avatarSrc = event.target.result;
        };
        reader.readAsDataURL(file);
      }
    }
  }
};
</script>
<style scoped>
.personal-container {
  padding: 20rpx;
  background-color: #f4f4f4;
}
.user-info {
  display: flex;
  margin-bottom: 30rpx;
}
.avatar-box {
  width: 20%;
}
.avatar {
  width: 80rpx;
  height: 80rpx;
  border-radius: 40rpx;
}
.username-box {
  width: 80%;
  display: flex;
  align-items: center;
}
.username {
  font-size: 36rpx;
  font-weight: bold;
}
.function-buttons {
  display: flex;
  justify-content: space-around;
}
.function-item {
  background-color: #fff;
  padding: 30rpx 20rpx;
  border-radius: 10rpx;
  box-shadow: 0 2rpx 5rpx rgba(0, 0, 0, 0.1);
}
</style>