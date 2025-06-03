<template>
  <div class="relative w-full overflow-hidden rounded-lg bg-black">
    <!-- 视频容器 -->
    <div class="relative aspect-video w-full">
      <!-- 视频元素 -->
      <video
        ref="videoRef"
        :src="src"
        :poster="poster"
        :autoplay="autoplay"
        :loop="loop"
        :muted="muted"
        class="h-full w-full object-contain"
        @timeupdate="handleTimeUpdate"
        @loadedmetadata="handleLoadedMetadata"
        @ended="handleEnded"
        @waiting="isBuffering = true"
        @playing="isBuffering = false"
      />

      <!-- 加载动画 -->
      <div
        v-if="isBuffering"
        class="absolute inset-0 flex items-center justify-center bg-black/50"
      >
        <div class="h-12 w-12 animate-spin rounded-full border-4 border-white border-t-transparent"></div>
      </div>

      <!-- 播放/暂停按钮 -->
      <button
        v-if="!isPlaying || showControls"
        class="absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2 rounded-full bg-white/10 p-4 text-white backdrop-blur-sm transition-all hover:bg-white/20"
        @click="togglePlay"
      >
        <svg
          v-if="!isPlaying"
          xmlns="http://www.w3.org/2000/svg"
          class="h-8 w-8"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z"
          />
        </svg>
        <svg
          v-else
          xmlns="http://www.w3.org/2000/svg"
          class="h-8 w-8"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M10 9v6m4-6v6"
          />
        </svg>
      </button>

      <!-- 控制栏 -->
      <div
        v-if="showControls"
        class="absolute bottom-0 left-0 right-0 flex items-center gap-2 bg-gradient-to-t from-black/50 p-4 text-white backdrop-blur-sm"
        @mouseenter="clearHideControlsTimer"
        @mouseleave="startHideControlsTimer"
      >
        <!-- 播放/暂停按钮 -->
        <button
          class="rounded-full p-1 hover:bg-white/10"
          @click="togglePlay"
        >
          <svg
            v-if="!isPlaying"
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
              d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z"
            />
          </svg>
          <svg
            v-else
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
              d="M10 9v6m4-6v6"
            />
          </svg>
        </button>

        <!-- 进度条 -->
        <div class="relative flex-1">
          <div
            class="h-1 cursor-pointer rounded-full bg-white/30"
            @click="handleProgressClick"
            ref="progressBarRef"
          >
            <div
              class="h-full rounded-full bg-white transition-all"
              :style="{ width: `${progress}%` }"
            ></div>
          </div>
        </div>

        <!-- 时间显示 -->
        <div class="text-sm">
          {{ formatTime(currentTime) }} / {{ formatTime(duration) }}
        </div>

        <!-- 音量控制 -->
        <div class="group relative flex items-center">
          <button
            class="rounded-full p-1 hover:bg-white/10"
            @click="toggleMute"
          >
            <svg
              v-if="!muted && volume > 0"
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
                d="M15.536 8.464a5 5 0 010 7.072M12 6v12m0-12l-4 4H4v4h4l4 4"
              />
            </svg>
            <svg
              v-else
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
                d="M5.586 15H4a1 1 0 01-1-1v-4a1 1 0 011-1h1.586l4.707-4.707C10.923 3.663 12 4.109 12 5v14c0 .891-1.077 1.337-1.707.707L5.586 15z"
                clip-rule="evenodd"
              />
            </svg>
          </button>
          <div class="invisible absolute -top-20 left-1/2 flex -translate-x-1/2 items-center rounded-lg bg-black/80 p-2 group-hover:visible">
            <input
              type="range"
              min="0"
              max="100"
              v-model="volume"
              class="h-1 w-20 cursor-pointer appearance-none rounded-full bg-white/30 [&::-webkit-slider-thumb]:h-3 [&::-webkit-slider-thumb]:w-3 [&::-webkit-slider-thumb]:appearance-none [&::-webkit-slider-thumb]:rounded-full [&::-webkit-slider-thumb]:bg-white"
            />
          </div>
        </div>

        <!-- 全屏按钮 -->
        <button
          class="rounded-full p-1 hover:bg-white/10"
          @click="toggleFullscreen"
        >
          <svg
            v-if="!isFullscreen"
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
              d="M4 8V4m0 0h4M4 4l5 5m11-1V4m0 0h-4m4 0l-5 5M4 16v4m0 0h4m-4 0l5-5m11 5l-5-5m5 5v-4m0 4h-4"
            />
          </svg>
          <svg
            v-else
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
              d="M9 9L4 4m0 0h5m-5 0v5m16-5l-5 5m5-5v5m0-5h-5M4 20v-5m0 5h5m-5 0l5-5m11 5l-5-5m5 5v-5m0 5h-5"
            />
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, watch } from 'vue'

// 定义组件属性
const props = defineProps({
  // 视频源地址
  src: {
    type: String,
    required: true
  },
  // 视频封面图
  poster: {
    type: String,
    default: ''
  },
  // 是否自动播放
  autoplay: {
    type: Boolean,
    default: false
  },
  // 是否循环播放
  loop: {
    type: Boolean,
    default: false
  },
  // 是否静音
  muted: {
    type: Boolean,
    default: false
  }
})

// 组件状态
const videoRef = ref(null)
const progressBarRef = ref(null)
const isPlaying = ref(false)
const isBuffering = ref(false)
const showControls = ref(false)
const isFullscreen = ref(false)
const currentTime = ref(0)
const duration = ref(0)
const volume = ref(100)
const hideControlsTimer = ref(null)

// 计算进度百分比
const progress = ref(0)

// 播放控制方法
const togglePlay = () => {
  if (videoRef.value) {
    if (isPlaying.value) {
      videoRef.value.pause()
    } else {
      videoRef.value.play()
    }
    isPlaying.value = !isPlaying.value
  }
}

// 静音控制
const toggleMute = () => {
  if (videoRef.value) {
    videoRef.value.muted = !videoRef.value.muted
  }
}

// 全屏控制
const toggleFullscreen = async () => {
  try {
    if (!document.fullscreenElement) {
      await videoRef.value.parentElement.requestFullscreen()
      isFullscreen.value = true
    } else {
      await document.exitFullscreen()
      isFullscreen.value = false
    }
  } catch (error) {
    console.error('全屏切换失败:', error)
  }
}

// 时间格式化
const formatTime = (seconds) => {
  const minutes = Math.floor(seconds / 60)
  const remainingSeconds = Math.floor(seconds % 60)
  return `${minutes}:${remainingSeconds.toString().padStart(2, '0')}`
}

// 进度条点击处理
const handleProgressClick = (event) => {
  if (!progressBarRef.value) return

  const rect = progressBarRef.value.getBoundingClientRect()
  const clickPosition = event.clientX - rect.left
  const percentage = (clickPosition / rect.width) * 100
  const newTime = (duration.value * percentage) / 100

  if (videoRef.value) {
    videoRef.value.currentTime = newTime
    progress.value = percentage
  }
}

// 视频事件处理
const handleTimeUpdate = () => {
  if (videoRef.value) {
    currentTime.value = videoRef.value.currentTime
    progress.value = (currentTime.value / duration.value) * 100
  }
}

const handleLoadedMetadata = () => {
  if (videoRef.value) {
    duration.value = videoRef.value.duration
  }
}

const handleEnded = () => {
  isPlaying.value = false
  if (props.loop) {
    videoRef.value.play()
  }
}

// 控制栏显示/隐藏
const startHideControlsTimer = () => {
  if (!isPlaying.value) return
  clearHideControlsTimer()
  hideControlsTimer.value = setTimeout(() => {
    showControls.value = false
  }, 2000)
}

const clearHideControlsTimer = () => {
  if (hideControlsTimer.value) {
    clearTimeout(hideControlsTimer.value)
    hideControlsTimer.value = null
  }
}

// 监听音量变化
const handleVolumeChange = () => {
  if (videoRef.value) {
    videoRef.value.volume = volume.value / 100
  }
}

// 监听鼠标移动
const handleMouseMove = () => {
  showControls.value = true
  startHideControlsTimer()
}

// 组件生命周期钩子
onMounted(() => {
  // 初始化音量
  if (videoRef.value) {
    videoRef.value.volume = volume.value / 100
  }

  // 添加事件监听
  document.addEventListener('mousemove', handleMouseMove)
  watch(volume, handleVolumeChange)

  // 监听全屏变化
  document.addEventListener('fullscreenchange', () => {
    isFullscreen.value = !!document.fullscreenElement
  })
})

onUnmounted(() => {
  // 清理事件监听
  document.removeEventListener('mousemove', handleMouseMove)
  document.removeEventListener('fullscreenchange', () => {})
  clearHideControlsTimer()
})
</script>
