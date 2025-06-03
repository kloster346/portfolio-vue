<template>
  <div
    class="inline-flex flex-col items-center justify-center"
    :class="[
      `loading-spinner--${type}`,
      `loading-spinner--${size}`,
      { 'fixed inset-0 bg-black bg-opacity-50 backdrop-blur-sm z-50': overlay }
    ]"
    :style="spinnerStyle"
  >
    <!-- 圆形旋转动画 -->
    <template v-if="type === 'circle'">
      <div class="relative w-8 h-8">
        <div class="absolute inset-0 border-4 border-transparent rounded-full loading-spinner__circle-inner"></div>
      </div>
    </template>

    <!-- 三点加载动画 -->
    <template v-else-if="type === 'dots'">
      <div class="flex gap-2">
        <div class="w-2 h-2 rounded-full loading-spinner__dot"></div>
        <div class="w-2 h-2 rounded-full loading-spinner__dot"></div>
        <div class="w-2 h-2 rounded-full loading-spinner__dot"></div>
      </div>
    </template>

    <!-- 脉冲动画 -->
    <template v-else-if="type === 'pulse'">
      <div class="w-8 h-8 rounded-full loading-spinner__pulse"></div>
    </template>

    <!-- 加载文本 -->
    <div v-if="text" class="mt-2 text-center" :style="textStyle">
      {{ text }}
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

// 定义组件属性
const props = defineProps({
  // 加载动画类型：circle（圆形旋转）、dots（三点）、pulse（脉冲）
  type: {
    type: String,
    default: 'circle',
    validator: (value) => ['circle', 'dots', 'pulse'].includes(value)
  },
  // 大小：small、medium、large
  size: {
    type: String,
    default: 'medium',
    validator: (value) => ['small', 'medium', 'large'].includes(value)
  },
  // 主色调
  color: {
    type: String,
    default: '#FFD700' // 默认金色
  },
  // 文本颜色
  textColor: {
    type: String,
    default: '#FFD700'
  },
  // 加载提示文本
  text: {
    type: String,
    default: ''
  },
  // 是否显示遮罩层
  overlay: {
    type: Boolean,
    default: false
  }
})

// 计算样式
const spinnerStyle = computed(() => ({
  '--spinner-color': props.color
}))

const textStyle = computed(() => ({
  color: props.textColor
}))
</script>

<style scoped>
/* 大小变体 */
.loading-spinner--small {
  font-size: 0.875rem;
}

.loading-spinner--medium {
  font-size: 1rem;
}

.loading-spinner--large {
  font-size: 1.125rem;
}

/* 圆形旋转动画 */
.loading-spinner__circle-inner {
  border-top-color: var(--spinner-color);
  animation: spin 0.8s linear infinite;
}

/* 三点加载动画 */
.loading-spinner__dot {
  background-color: var(--spinner-color);
  animation: pulse 1s ease-in-out infinite;
}

.loading-spinner__dot:nth-child(2) {
  animation-delay: 0.2s;
}

.loading-spinner__dot:nth-child(3) {
  animation-delay: 0.4s;
}

/* 脉冲动画 */
.loading-spinner__pulse {
  background-color: var(--spinner-color);
  animation: pulse-ring 1.25s cubic-bezier(0.215, 0.61, 0.355, 1) infinite;
}

/* 动画关键帧 */
@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

@keyframes pulse {
  0%, 100% {
    transform: scale(0.5);
    opacity: 0.2;
  }
  50% {
    transform: scale(1);
    opacity: 1;
  }
}

@keyframes pulse-ring {
  0% {
    transform: scale(0.33);
    opacity: 1;
  }
  80%, 100% {
    transform: scale(1);
    opacity: 0;
  }
}

/* 大小变体对应的具体尺寸 */
.loading-spinner--small .loading-spinner__circle,
.loading-spinner--small .loading-spinner__pulse {
  width: 1.5rem;
  height: 1.5rem;
}

.loading-spinner--small .loading-spinner__dot {
  width: 0.375rem;
  height: 0.375rem;
}

.loading-spinner--large .loading-spinner__circle,
.loading-spinner--large .loading-spinner__pulse {
  width: 2.5rem;
  height: 2.5rem;
}

.loading-spinner--large .loading-spinner__dot {
  width: 0.625rem;
  height: 0.625rem;
}
</style>
