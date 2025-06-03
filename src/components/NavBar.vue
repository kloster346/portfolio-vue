<template>
  <nav class="bg-black bg-opacity-90 backdrop-blur-sm border-b border-gold-500 border-opacity-20">
    <div class="max-w-7xl mx-auto px-6 lg:px-8">
      <div class="flex justify-between items-center h-16">
        <!-- Logo 区域 -->
        <div class="flex-shrink-0">
          <router-link to="/" class="flex items-center space-x-3 hover:opacity-80 transition-opacity duration-300">
            <!-- Logo 图标 -->
            <div class="w-10 h-10 bg-gradient-to-br from-gold-400 to-gold-600 rounded-lg flex items-center justify-center">
              <span class="text-black font-bold text-lg">农</span>
            </div>
            <!-- Logo 文字 -->
            <div class="hidden sm:block">
              <h1 class="text-xl font-bold text-white">农淑惠</h1>
              <p class="text-xs text-gold-400 -mt-1">作品集</p>
            </div>
          </router-link>
        </div>

        <!-- 导航菜单 -->
        <div class="hidden md:block">
          <div class="ml-10 flex items-baseline space-x-8">
            <router-link
              v-for="item in navigationItems"
              :key="item.name"
              :to="item.path"
              class="nav-link"
              :class="{
                'nav-link-active': $route.path === item.path,
                'nav-link-inactive': $route.path !== item.path
              }"
            >
              {{ item.name }}
            </router-link>
          </div>
        </div>

        <!-- 移动端菜单按钮（暂时隐藏，因为只做PC端） -->
        <div class="md:hidden">
          <button
            @click="toggleMobileMenu"
            class="text-gray-300 hover:text-white focus:outline-none focus:text-white transition-colors duration-200"
            style="display: none;"
          >
            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import { ref, computed } from 'vue'
import { useRoute } from 'vue-router'

/**
 * NavBar 顶部导航栏组件
 *
 * 功能说明：
 * - 提供网站主要导航功能
 * - 包含Logo区域和品牌标识
 * - 响应式导航菜单（专为PC端优化）
 * - 当前页面高亮显示
 * - 黑金主题设计
 *
 * 导航结构：
 * - 首页：展示个人介绍和特色作品
 * - 作品集：分类展示所有作品
 * - 关于我：详细个人信息和技能
 *
 * 样式特点：
 * - 半透明黑色背景with毛玻璃效果
 * - 金色边框和强调色
 * - 悬停和激活状态的视觉反馈
 */
export default {
  name: 'NavBar',

  setup() {
    const route = useRoute()
    const isMobileMenuOpen = ref(false)

    // 导航菜单项配置
    const navigationItems = ref([
      {
        name: '首页',
        path: '/',
        description: '个人介绍和特色作品展示'
      },
      {
        name: '作品集',
        path: '/portfolio',
        description: 'MG动画、PR剪辑、平面设计等作品'
      },
      {
        name: '关于我',
        path: '/about',
        description: '个人经历、技能和联系方式'
      }
    ])

    // 移动端菜单切换（预留功能）
    const toggleMobileMenu = () => {
      isMobileMenuOpen.value = !isMobileMenuOpen.value
    }

    // 当前激活的导航项
    const activeNavItem = computed(() => {
      return navigationItems.value.find(item => item.path === route.path)
    })

    return {
      navigationItems,
      isMobileMenuOpen,
      toggleMobileMenu,
      activeNavItem
    }
  }
}
</script>

<style scoped>
/* 导航栏基础样式 */
nav {
  position: sticky;
  top: 0;
  z-index: 50;
  transition: all 0.3s ease;
}

/* 导航链接基础样式 */
.nav-link {
  padding: 0.75rem 0.75rem;
  border-radius: 0.375rem;
  font-size: 0.875rem;
  font-weight: 500;
  transition: all 0.2s ease;
  position: relative;
}

/* 未激活状态的导航链接 */
.nav-link-inactive {
  color: #D1D5DB;
}

.nav-link-inactive:hover {
  color: #FFFFFF;
  background-color: rgba(55, 65, 81, 0.5);
}

/* 激活状态的导航链接 */
.nav-link-active {
  color: #FBBF24;
  background-color: rgba(245, 158, 11, 0.1);
}

/* 激活状态下的底部金色线条 */
.nav-link-active::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 50%;
  transform: translateX(-50%);
  width: 80%;
  height: 2px;
  background: linear-gradient(90deg, transparent, #FFD700, transparent);
  border-radius: 1px;
}

/* 悬停效果增强 */
.nav-link:hover {
  transform: translateY(-1px);
}

/* Logo悬停效果 */
.flex-shrink-0 a:hover .w-10 {
  transform: scale(1.05);
  transition: transform 0.2s ease;
}

/* 自定义金色主题类 */
.text-gold-400 {
  color: #FBBF24;
}

.text-gold-600 {
  color: #D97706;
}

.border-gold-500 {
  border-color: #F59E0B;
}

.bg-gold-400 {
  background-color: #FBBF24;
}

.bg-gold-500 {
  background-color: #F59E0B;
}

.bg-gold-600 {
  background-color: #D97706;
}

/* PC端专用样式优化 */
@media (min-width: 1024px) {
  .max-w-7xl {
    max-width: 1280px;
  }

  .nav-link {
    font-size: 0.95rem;
    padding: 0.75rem 1rem;
  }

  /* 导航栏在大屏幕上的额外间距 */
  .ml-10 {
    margin-left: 3rem;
  }
}
</style>
