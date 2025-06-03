<template>
  <div>
    <!-- 触发器 -->
    <div class="cursor-pointer" @click="showViewer = true">
      <slot></slot>
    </div>

    <!-- 图片查看器 -->
    <Teleport to="body">
      <div
        v-if="showViewer"
        class="fixed inset-0 z-50 flex items-center justify-center bg-black/90 backdrop-blur-sm"
        @click.self="closeViewer"
      >
        <!-- 关闭按钮 -->
        <button
          class="absolute right-4 top-4 rounded-full bg-white/10 p-2 text-white hover:bg-white/20"
          @click="closeViewer"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M6 18L18 6M6 6l12 12"
            />
          </svg>
        </button>

        <!-- 导航按钮 - 上一张 -->
        <button
          v-if="showNavigation"
          class="absolute left-4 top-1/2 -translate-y-1/2 rounded-full bg-white/10 p-2 text-white hover:bg-white/20"
          @click="previousImage"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M15 19l-7-7 7-7"
            />
          </svg>
        </button>

        <!-- 图片容器 -->
        <div class="relative max-h-[90vh] max-w-[90vw]">
          <img
            :src="currentImage"
            :alt="currentAlt"
            class="h-auto max-h-[90vh] w-auto max-w-[90vw] object-contain"
            @load="imageLoaded = true"
          />
          <!-- 加载动画 -->
          <div
            v-if="!imageLoaded"
            class="absolute inset-0 flex items-center justify-center"
          >
            <div class="h-8 w-8 animate-spin rounded-full border-4 border-white border-t-transparent"></div>
          </div>
        </div>

        <!-- 导航按钮 - 下一张 -->
        <button
          v-if="showNavigation"
          class="absolute right-4 top-1/2 -translate-y-1/2 rounded-full bg-white/10 p-2 text-white hover:bg-white/20"
          @click="nextImage"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M9 5l7 7-7 7"
            />
          </svg>
        </button>
      </div>
    </Teleport>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

// 定义组件属性
const props = defineProps({
  // 图片数组，每个元素包含 src 和 alt
  images: {
    type: Array,
    default: () => []
  },
  // 当前显示的图片索引
  initialIndex: {
    type: Number,
    default: 0
  }
})

// 组件状态
const showViewer = ref(false)
const currentIndex = ref(props.initialIndex)
const imageLoaded = ref(false)

// 计算属性
const showNavigation = computed(() => props.images.length > 1)
const currentImage = computed(() => props.images[currentIndex.value]?.src || '')
const currentAlt = computed(() => props.images[currentIndex.value]?.alt || '')

// 方法
const closeViewer = () => {
  showViewer.value = false
  imageLoaded.value = false
}

const previousImage = () => {
  imageLoaded.value = false
  currentIndex.value = currentIndex.value > 0 ? currentIndex.value - 1 : props.images.length - 1
}

const nextImage = () => {
  imageLoaded.value = false
  currentIndex.value = currentIndex.value < props.images.length - 1 ? currentIndex.value + 1 : 0
}

// 键盘事件处理
const handleKeydown = (event) => {
  if (!showViewer.value) return

  switch (event.key) {
    case 'Escape':
      closeViewer()
      break
    case 'ArrowLeft':
      if (showNavigation.value) previousImage()
      break
    case 'ArrowRight':
      if (showNavigation.value) nextImage()
      break
  }
}

// 添加和移除键盘事件监听器
onMounted(() => {
  document.addEventListener('keydown', handleKeydown)
})

onUnmounted(() => {
  document.removeEventListener('keydown', handleKeydown)
})
</script>
