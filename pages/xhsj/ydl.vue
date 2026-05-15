<template>
  <view class="container">
    <view class="userInfo">
      <view class="avatar">
        <text class="avatarText">头像</text>
      </view>
      <view class="info">
        <text class="name">姓名：测试账户</text>
        <text class="gender">性别：男</text>
        <text class="phone">电话：139****1234</text>
        <text class="address">地址：XX省XX市XX区XX街道XX号</text>
      </view>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {};
    },
  };
</script>

<style>
  .container {
    flex: 1;
    background-color: #fff;
    padding: 20px;
  }

  .userInfo {
    display: flex;
    flex-direction: row;
    align-items: center;
  }

  .avatar {
    width: 80px;
    height: 80px;
    border-radius: 40px;
    background-color: #ccc;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .avatarText {
    font-size: 20px;
    font-weight: bold;
  }

  .info {
    margin-left: 20px;
  }

  .name {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 10px;
  }

  .gender {
    font-size: 16px;
    margin-bottom: 10px;
  }

  .phone {
    font-size: 16px;
    margin-bottom: 10px;
  }

  .address {
    font-size: 16px;
  }
</style>