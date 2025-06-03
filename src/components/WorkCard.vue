<template>
  <div
    class="work-card group relative overflow-hidden rounded-lg bg-gray-900 transition-transform duration-300 hover:scale-[1.02] hover:shadow-xl"
    @click="$emit('click')"
  >
    <!-- 图片容器 -->
    <div class="aspect-video overflow-hidden">
      <img
        :src="props.imageUrl"
        :alt="props.title"
        class="h-full w-full object-cover transition-transform duration-500 group-hover:scale-110"
        loading="lazy"
      />
    </div>

    <!-- 内容遮罩层 -->
    <div class="absolute inset-0 bg-gradient-to-t from-black/90 to-transparent opacity-0 transition-opacity duration-300 group-hover:opacity-100">
      <!-- 作品信息 -->
      <div class="absolute bottom-0 w-full p-4 text-white">
        <h3 class="mb-2 text-xl font-bold">{{ props.title }}</h3>
        <p class="text-sm text-gray-300">{{ props.description }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

// 定义组件属性
const props = defineProps({
  imageUrl: {
    type: String,
    required: true
  },
  title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    default: ''
  }
})

// 定义事件
defineEmits(['click'])
</script>
