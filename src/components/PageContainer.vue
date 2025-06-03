<template>
  <div class="page-container">
    <!-- 页面头部区域 -->
    <header v-if="showHeader" class="page-header">
      <div class="header-content">
        <h1 v-if="title" class="page-title">{{ title }}</h1>
        <p v-if="subtitle" class="page-subtitle">{{ subtitle }}</p>
      </div>
    </header>

    <!-- 页面主要内容区域 -->
    <main class="page-main">
      <div class="main-content">
        <slot></slot>
      </div>
    </main>

    <!-- 页面底部区域（可选） -->
    <footer v-if="showFooter" class="page-footer">
      <slot name="footer"></slot>
    </footer>
  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'PageContainer',
  props: {
    // 页面标题
    title: {
      type: String,
      default: ''
    },
    // 页面副标题
    subtitle: {
      type: String,
      default: ''
    },
    // 是否显示页面头部
    showHeader: {
      type: Boolean,
      default: true
    },
    // 是否显示页面底部
    showFooter: {
      type: Boolean,
      default: false
    },
    // 容器最大宽度
    maxWidth: {
      type: String,
      default: '1200px'
    },
    // 内容区域内边距
    padding: {
      type: String,
      default: '2rem'
    },
    // 是否启用全屏模式
    fullscreen: {
      type: Boolean,
      default: false
    },
    // 背景样式类型
    backgroundType: {
      type: String,
      default: 'default', // default, gradient, transparent
      validator: (value) => ['default', 'gradient', 'transparent'].includes(value)
    }
  },
  computed: {
    // 动态计算容器样式
    containerStyles() {
      return {
        '--max-width': this.maxWidth,
        '--content-padding': this.padding
      }
    },
    // 动态计算容器类名
    containerClasses() {
      return [
        'page-container',
        `bg-${this.backgroundType}`,
        {
          'fullscreen': this.fullscreen
        }
      ]
    }
  }
})
</script>

<style scoped>
/* 页面容器基础样式 */
.page-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  width: 100%;
  position: relative;
}

/* 背景样式变体 */
.page-container.bg-default {
  background-color: #1a1a1a;
}

.page-container.bg-gradient {
  background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 100%);
}

.page-container.bg-transparent {
  background: transparent;
}

/* 全屏模式 */
.page-container.fullscreen {
  height: 100vh;
  overflow: hidden;
}

/* 页面头部样式 */
.page-header {
  padding: 2rem 0 1rem;
  border-bottom: 1px solid rgba(255, 215, 0, 0.2);
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(10px);
}

.header-content {
  max-width: var(--max-width, 1200px);
  margin: 0 auto;
  padding: 0 var(--content-padding, 2rem);
  text-align: center;
}

.page-title {
  font-size: 2.5rem;
  font-weight: 700;
  color: #FFD700;
  margin: 0 0 0.5rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
  letter-spacing: 1px;
}

.page-subtitle {
  font-size: 1.2rem;
  color: #cccccc;
  margin: 0;
  font-weight: 300;
  opacity: 0.9;
}

/* 主要内容区域 */
.page-main {
  flex: 1;
  display: flex;
  flex-direction: column;
  width: 100%;
}

.main-content {
  max-width: var(--max-width, 1200px);
  margin: 0 auto;
  padding: var(--content-padding, 2rem);
  width: 100%;
  flex: 1;
  display: flex;
  flex-direction: column;
}

/* 页面底部样式 */
.page-footer {
  padding: 1rem 0;
  border-top: 1px solid rgba(255, 215, 0, 0.2);
  background: rgba(0, 0, 0, 0.3);
  margin-top: auto;
}

/* PC端适配 */
@media (min-width: 1024px) {
  .page-header {
    padding: 3rem 0 2rem;
  }

  .page-title {
    font-size: 3rem;
  }

  .page-subtitle {
    font-size: 1.4rem;
  }

  .main-content {
    padding: 3rem 2rem;
  }
}

/* 大屏幕适配 */
@media (min-width: 1440px) {
  .page-title {
    font-size: 3.5rem;
  }

  .main-content {
    padding: 4rem 2rem;
  }
}

/* 响应式调整 */
@media (max-width: 768px) {
  .page-title {
    font-size: 2rem;
  }

  .page-subtitle {
    font-size: 1rem;
  }

  .main-content {
    padding: 1.5rem 1rem;
  }

  .header-content {
    padding: 0 1rem;
  }
}

/* 动画效果 */
.page-header {
  animation: fadeInDown 0.6s ease-out;
}

.main-content {
  animation: fadeInUp 0.8s ease-out;
}

@keyframes fadeInDown {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* 滚动条样式 */
.page-container::-webkit-scrollbar {
  width: 8px;
}

.page-container::-webkit-scrollbar-track {
  background: rgba(0, 0, 0, 0.1);
}

.page-container::-webkit-scrollbar-thumb {
  background: rgba(255, 215, 0, 0.3);
  border-radius: 4px;
}

.page-container::-webkit-scrollbar-thumb:hover {
  background: rgba(255, 215, 0, 0.5);
}
</style>
