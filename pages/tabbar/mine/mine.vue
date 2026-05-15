<template>
  <view class="login-container">
    <!-- 使用 scroll-view 包裹内容 -->
    <scroll-view scroll-y="true" :style="{ height: scrollHeight + 'px' }">
      <!-- 标题 -->
      <view class="login-title">{{ isRegister ? '注册' : '登录' }}</view>

      <!-- 用户名输入框 -->
      <view class="input-group">
        <uni-icons class="input-icon" type="person" size="20" color="#999" />
        <input
          class="input-field"
          type="text"
          placeholder="请输入用户名"
          v-model="username"
        />
      </view>

      <!-- 密码输入框 -->
      <view class="input-group">
        <uni-icons class="input-icon" type="locked" size="20" color="#999" />
        <input
          class="input-field"
          type="password"
          placeholder="请输入密码"
          v-model="password"
        />
      </view>

      <!-- 登录/注册按钮 -->
      <button class="login-button" @click="handleSubmit">
        {{ isRegister ? '注册' : '登录' }}
      </button>

      <!-- 切换登录/注册链接 -->
      <view class="register-link">
        <text>{{ isRegister ? '已有账号？' : '还没有账号？' }}</text>
        <text class="link-text" @click="toggleMode">
          {{ isRegister ? '去登录' : '立即注册' }}
        </text>
      </view>
    </scroll-view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      username: "", // 用户名
      password: "", // 密码
      isRegister: false, // 是否为注册模式
      scrollHeight: 0, // 滚动区域高度
    };
  },
  mounted() {
    // 获取屏幕高度并设置 scroll-view 高度
    uni.getSystemInfo({
      success: (res) => {
        this.scrollHeight = res.windowHeight;
      },
    });
  },
  methods: {
    // 处理登录/注册
    handleSubmit() {
      if (!this.username || !this.password) {
        uni.showToast({
          title: "请输入用户名和密码",
          icon: "none",
        });
        return;
      }

      if (this.isRegister) {
        this.handleRegister(); // 注册
      } else {
        this.handleLogin(); // 登录
      }
    },

    // 处理登录
    handleLogin() {
      const users = uni.getStorageSync("users") || [];
      const user = users.find(
        (u) => u.username === this.username && u.password === this.password
      );
    
      if (user) {
        uni.showToast({
          title: "登录成功",
          icon: "success",
        });
    
        // 仅修改这里：跳转到个人中心页面
        setTimeout(() => {
          uni.navigateTo({
            url: "/pages/personal/personal",
          });
        }, 1500);
      } else {
        uni.showToast({
          title: "用户名或密码错误",
          icon: "none",
        });
      }
    },

    // 处理注册
    handleRegister() {
      const users = uni.getStorageSync("users") || [];

      // 检查用户名是否已存在
      const userExists = users.some((u) => u.username === this.username);
      if (userExists) {
        uni.showToast({
          title: "用户名已存在",
          icon: "none",
        });
        return;
      }

      // 添加新用户
      users.push({
        username: this.username,
        password: this.password,
      });
      uni.setStorageSync("users", users);

      uni.showToast({
        title: "注册成功",
        icon: "success",
      });

      // 切换到登录模式
      this.isRegister = false;
      this.username = "";
      this.password = "";
    },

    // 切换登录/注册模式
    toggleMode() {
      this.isRegister = !this.isRegister;
      this.username = "";
      this.password = "";
    },
  },
};
</script>

<style lang="scss">
.login-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  padding: 20px;
  background-color: #f8f9fa;
}

.login-title {
  font-size: 24px;
  font-weight: bold;
  color: #333;
  margin-bottom: 40px;
}

.input-group {
  display: flex;
  align-items: center;
  width: 100%;
  height: 50px;
  background-color: #fff;
  border: 1px solid #e0e0e0;
  border-radius: 25px;
  padding: 0 15px;
  margin-bottom: 20px;
}

.input-icon {
  margin-right: 10px;
}

.input-field {
  flex: 1;
  height: 100%;
  font-size: 14px;
  color: #333;
  background-color: transparent;
  border: none;
  outline: none;

  &::placeholder {
    color: #999;
  }
}

.login-button {
  width: 100%;
  height: 50px;
  background-color: #77c78c;
  color: #fff;
  font-size: 16px;
  border-radius: 25px;
  margin-top: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: none;
  outline: none;
  cursor: pointer;

  &:active {
    background-color: #77c78c;
  }
}

.register-link {
  margin-top: 20px;
  font-size: 14px;
  color: #666;

  .link-text {
    color: #77c78c;
    margin-left: 5px;
    cursor: pointer;

    &:active {
      color: #77c78c;
    }
  }
}
</style>