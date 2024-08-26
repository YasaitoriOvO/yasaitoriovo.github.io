<template>
  <div class="container">
    <div class="avatar-container">
      <div class="ripple"></div> <!-- 水波效果容器 -->
      <img src="./assets/logo.png" class="avatar" />
    </div>
    <div class="name-container">
      <div class="name-wrapper">
        <div class="name">
          <span class="main-text">菜</span>
          <span class="small-text">やさい</span>
        </div>
        <div class="name">
          <span class="main-text">鸡</span>
          <span class="small-text">とり</span>
        </div>
      </div>
    </div>
    <!-- 图标容器 -->
    <div class="icon-container">
      <div class="icon-wrapper">
        <div class="icon doc-icon" @click="navigateTo('https://linktr.ee/yasaitori')"></div>
        <div class="icon link-icon" @click="navigateTo('https://yatori.fun/links')"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  mounted() {
    // 延迟设置水波效果的可见性，确保头像滑入后才开始显示水波效果
    setTimeout(() => {
      const ripple = document.querySelector('.ripple');
      if (ripple) {
        ripple.style.visibility = 'visible';
        ripple.style.animationPlayState = 'running'; // 启动水波动画
      }
    }, 1000); // 这里的1000ms应该与头像滑入动画的时长匹配
  },
  methods: {
    navigateTo(url) {
      window.location.href = url; // 使用 window.location.href 跳转到外部网站
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #ffffff;
  overflow: hidden; /* 防止水波纹溢出 */
}

.avatar-container {
  position: relative;
  animation: slideInFromLeft 1s ease-in-out forwards; /* forwards 确保动画结束后保持最终状态 */
}

.avatar {
  width: 300px; /* 增大头像尺寸 */
  height: 300px;
  border-radius: 50%;
  background-color: #e0d8f9;
  animation: rotateInfinite 4s linear infinite; /* 无需延迟或中断的持续旋转 */
}

.name-container {
  margin-top: 20px;
  animation: slideInFromBottom 1s ease-in-out;
  text-align: center; /* 使字体居中 */
}

.name-wrapper {
  display: flex; /* 使用 Flexbox 排列子元素 */
  justify-content: center; /* 水平居中对齐 */
  gap: 40px; /* 调整两个名字之间的间距 */
}

.name {
  display: inline-block; /* 保持名字垂直对齐 */
  position: relative;
}

.main-text {
  font-family: "Noto Sans SC", sans-serif;
  font-optical-sizing: auto;
  font-weight: 900;
  font-style: normal;
  font-size: 60px; /* 增大字体尺寸 */
  color: #3c3c3c;
}

.small-text {
  font-family: "Noto Sans SC", sans-serif;
  font-optical-sizing: auto;
  font-weight: 900;
  font-style: normal;
  display: block;
  font-size: 1em; /* 缩小字体尺寸 */
  color: #3c3c3c;
  position: absolute;
  left: 50%;
  transform: translateX(-200%);
  top: 1em; /* 根据实际需要调整位置 */
}

/* 图标样式 */
.icon-container {
  margin-top: 40px;
  display: flex;
  justify-content: center;
}

.icon-wrapper {
  display: flex;
  gap: 40px; /* 图标间距 */
}

.icon {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  position: relative;
  cursor: pointer;
  background-size: cover;
  transition: background-color 0.3s ease, transform 0.3s ease; /* 添加transform过渡效果 */
}

/* 鼠标悬停时的圆形背景与缩小效果 */
.icon:hover {
  transform: scale(0.9); /* 缩小图标 */
}

.icon:hover::before {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  width: 80px;
  height: 80px;
  background-color: rgba(100, 100, 100, 0.3);
  border-radius: 50%;
  transform: translate(-50%, -50%) scale(0);
  z-index: -1;
  transition: transform 0.3s ease;
}

.icon:hover::before {
  transform: translate(-50%, -50%) scale(1);
}

/* 文档图标和链接图标的具体样式 */
.doc-icon {
  background-image: url('./assets/doc.png'); /* 替换为实际文档图标路径 */
  animation: slideInFromRight 1s ease-in-out forwards;
}

.link-icon {
  background-image: url('./assets/link.png'); /* 替换为实际链接图标路径 */
  animation: slideInFromRight 1s ease-in-out forwards;
  animation-delay: 100ms;
}


@keyframes slideInFromLeft {
  from {
    transform: translateX(-350%);
  }
  to {
    transform: translateX(0);
  }
}

@keyframes slideInFromRight {
  from {
    transform: translateX(2000%);
  }
  to {
    transform: translateX(0);
  }
}

@keyframes rotateInfinite {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

@keyframes slideInFromBottom {
  from {
    transform: translateY(100%);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.ripple {
  position: absolute;
  width: 400px; /* 水波纹的大小 */
  height: 400px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: rgba(224, 216, 249, 0.5);
  border-radius: 50%;
  z-index: -1; /* 置于头像后方 */
  visibility: hidden; /* 初始状态下隐藏 */
  animation: rippleEffect 1s ease-out infinite;
  animation-play-state: paused; /* 初始状态暂停动画 */
}

@keyframes rippleEffect {
  0% {
    transform: translate(-50%, -50%) scale(0.8);
    opacity: 1;
  }
  100% {
    transform: translate(-50%, -50%) scale(1.5);
    opacity: 0;
  }
}
</style>
