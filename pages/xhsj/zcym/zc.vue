<template>
  <div>
    <input type="text" v-model="username" placeholder="用户名">
    <input type="password" v-model="password" placeholder="密码">
    <button @click="register">注册</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: ''
    }
  },
  methods: {
    register() {
      // 将用户名和密码保存到本地存储或数据库中
      uni.setStorageSync('username', this.username);
      uni.setStorageSync('password', this.password);
      
      // 跳转到登录页面
      uni.navigateTo({
        url: '/pages/tabbar/mine/mine'
      });
    }
  }
}
</script>