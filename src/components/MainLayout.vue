<template>
  <div class="min-h-screen bg-gray-900 text-white">
    <!-- 主布局容器 -->
    <div class="flex flex-col min-h-screen">
      <!-- 顶部导航栏区域 -->
      <header class="flex-shrink-0">
        <slot name="header">
          <!-- 默认头部内容，可被具体页面覆盖 -->
        </slot>
      </header>

      <!-- 主内容区域 -->
      <main class="flex-1">
        <slot name="main">
          <!-- 主要内容区域 -->
          <slot></slot>
        </slot>
      </main>

      <!-- 页脚区域 -->
      <footer class="flex-shrink-0">
        <slot name="footer">
          <!-- 默认页脚内容，可被具体页面覆盖 -->
        </slot>
      </footer>
    </div>
  </div>
</template>

<script>
/**
 * MainLayout 主布局组件
 *
 * 功能说明：
 * - 提供整个应用的主要布局结构
 * - 采用 Flexbox 布局，确保页脚始终在底部
 * - 使用插槽系统，允许页面自定义头部、主内容和页脚
 * - 应用黑金主题的基础样式
 *
 * 使用方法：
 * <MainLayout>
 *   <template #header>自定义头部内容</template>
 *   <template #main>主要内容</template>
 *   <template #footer>自定义页脚内容</template>
 * </MainLayout>
 */
export default {
  name: 'MainLayout',

  setup() {
    // 主布局组件的逻辑处理
    // 目前为基础版本，后续可根据需要添加响应式逻辑

    return {
      // 返回响应式数据和方法
    }
  }
}
</script>

<style scoped>
/* 主布局样式 - 专为PC端设计 */
.min-h-screen {
  /* 确保布局至少占满整个视口高度 */
  min-height: 100vh;
}

/* PC端专用样式 */
@media (min-width: 1024px) {
  /* 可根据需要添加桌面端特定样式 */
  .flex-col {
    /* 桌面端垂直布局优化 */
    gap: 0;
  }
}
</style>
