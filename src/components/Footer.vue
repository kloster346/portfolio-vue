<template>
  <footer class="bg-black bg-opacity-95 border-t border-gold-500 border-opacity-20 mt-auto">
    <div class="max-w-7xl mx-auto px-6 lg:px-8 py-12">
      <!-- 主要内容区域 -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-8">
        <!-- 个人信息区域 -->
        <div class="space-y-4">
          <div class="flex items-center space-x-3">
            <div class="w-8 h-8 bg-gradient-to-br from-gold-400 to-gold-600 rounded-lg flex items-center justify-center">
              <span class="text-black font-bold text-sm">农</span>
            </div>
            <h3 class="text-xl font-bold text-white">农淑惠</h3>
          </div>
          <p class="text-gray-300 text-sm leading-relaxed">
            专注于MG动画、视频剪辑和平面设计的创意工作者，
            致力于用视觉艺术传达美好故事。
          </p>
          <div class="flex items-center space-x-2 text-gold-400">
            <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
              <path fill-rule="evenodd" d="M5.05 4.05a7 7 0 119.9 9.9L10 18.9l-4.95-4.95a7 7 0 010-9.9zM10 11a2 2 0 100-4 2 2 0 000 4z" clip-rule="evenodd" />
            </svg>
            <span class="text-sm text-gray-300">中国·广西</span>
          </div>
        </div>

        <!-- 技能标签区域 -->
        <div class="space-y-4">
          <h4 class="text-lg font-semibold text-white">专业技能</h4>
          <div class="flex flex-wrap gap-2">
            <span
              v-for="skill in skills"
              :key="skill"
              class="px-3 py-1 bg-gold-500 bg-opacity-10 text-gold-400 text-xs rounded-full border border-gold-500 border-opacity-30 hover:bg-opacity-20 transition-all duration-200"
            >
              {{ skill }}
            </span>
          </div>
        </div>

        <!-- 联系方式区域 -->
        <div class="space-y-4">
          <h4 class="text-lg font-semibold text-white">联系方式</h4>
          <div class="space-y-3">
            <a
              v-for="contact in contactInfo"
              :key="contact.type"
              :href="contact.link"
              class="flex items-center space-x-3 text-gray-300 hover:text-gold-400 transition-colors duration-200 group"
            >
              <div class="w-5 h-5 text-gold-500 group-hover:scale-110 transition-transform duration-200">
                <component :is="contact.icon" />
              </div>
              <span class="text-sm">{{ contact.label }}</span>
            </a>
          </div>
        </div>
      </div>

      <!-- 分割线 -->
      <div class="border-t border-gray-700 border-opacity-50 pt-8">
        <!-- 底部版权信息 -->
        <div class="flex flex-col md:flex-row justify-between items-center space-y-4 md:space-y-0">
          <div class="text-center md:text-left">
            <p class="text-gray-400 text-sm">
              © {{ currentYear }} 农淑惠作品集. 保留所有权利.
            </p>
            <p class="text-gray-500 text-xs mt-1">
              Built with Vue.js & Tailwind CSS
            </p>
          </div>

          <!-- 社交媒体链接 -->
          <div class="flex items-center space-x-4">
            <a
              v-for="social in socialLinks"
              :key="social.name"
              :href="social.url"
              :title="social.name"
              class="w-8 h-8 bg-gray-800 hover:bg-gold-500 text-gray-400 hover:text-black rounded-full flex items-center justify-center transition-all duration-200 hover:scale-110"
              target="_blank"
              rel="noopener noreferrer"
            >
              <component :is="social.icon" class="w-4 h-4" />
            </a>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import { ref, computed } from 'vue'

/**
 * Footer 页脚组件
 *
 * 功能说明：
 * - 展示个人品牌信息和简介
 * - 显示专业技能标签
 * - 提供多种联系方式
 * - 包含社交媒体链接
 * - 版权信息和技术栈说明
 *
 * 设计特点：
 * - 黑金主题配色方案
 * - 响应式网格布局（PC端优化）
 * - 悬停交互效果
 * - 图标和视觉元素增强
 *
 * 布局结构：
 * - 三列网格：个人信息 | 技能标签 | 联系方式
 * - 底部区域：版权信息 | 社交媒体链接
 */
export default {
  name: 'AppFooter',

  setup() {
    // 当前年份
    const currentYear = computed(() => new Date().getFullYear())

    // 专业技能列表
    const skills = ref([
      'MG动画',
      'After Effects',
      'Premiere Pro',
      '平面设计',
      'Photoshop',
      'Illustrator',
      '视频剪辑',
      '动效设计',
      '品牌设计'
    ])

    // 联系方式信息
    const contactInfo = ref([
      {
        type: 'email',
        label: 'hello@example.com',
        link: 'mailto:hello@example.com',
        icon: 'EmailIcon'
      },
      {
        type: 'phone',
        label: '+86 138-0000-0000',
        link: 'tel:+8613800000000',
        icon: 'PhoneIcon'
      },
      {
        type: 'wechat',
        label: '微信咨询',
        link: '#',
        icon: 'WechatIcon'
      }
    ])

    // 社交媒体链接
    const socialLinks = ref([
      {
        name: '微博',
        url: 'https://weibo.com',
        icon: 'WeiboIcon'
      },
      {
        name: '抖音',
        url: 'https://douyin.com',
        icon: 'DouyinIcon'
      },
      {
        name: 'B站',
        url: 'https://bilibili.com',
        icon: 'BilibiliIcon'
      },
      {
        name: 'GitHub',
        url: 'https://github.com',
        icon: 'GithubIcon'
      }
    ])

    return {
      currentYear,
      skills,
      contactInfo,
      socialLinks
    }
  },

  components: {
    // 邮箱图标
    EmailIcon: {
      template: `
        <svg fill="currentColor" viewBox="0 0 20 20">
          <path d="M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884z" />
          <path d="M18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z" />
        </svg>
      `
    },
    // 电话图标
    PhoneIcon: {
      template: `
        <svg fill="currentColor" viewBox="0 0 20 20">
          <path d="M2 3a1 1 0 011-1h2.153a1 1 0 01.986.836l.74 4.435a1 1 0 01-.54 1.06l-1.548.773a11.037 11.037 0 006.105 6.105l.774-1.548a1 1 0 011.059-.54l4.435.74a1 1 0 01.836.986V17a1 1 0 01-1 1h-2C7.82 18 2 12.18 2 5V3z" />
        </svg>
      `
    },
    // 微信图标
    WechatIcon: {
      template: `
        <svg fill="currentColor" viewBox="0 0 20 20">
          <path d="M10 2C5.58 2 2 5.58 2 10s3.58 8 8 8 8-3.58 8-8-3.58-8-8-8zm3.5 6L10 10.5 6.5 8 10 5.5 13.5 8z" />
        </svg>
      `
    },
    // 微博图标
    WeiboIcon: {
      template: `
        <svg fill="currentColor" viewBox="0 0 20 20">
          <path d="M10 18a8 8 0 100-16 8 8 0 000 16zM7 9a1 1 0 000 2h6a1 1 0 100-2H7z" />
        </svg>
      `
    },
    // 抖音图标
    DouyinIcon: {
      template: `
        <svg fill="currentColor" viewBox="0 0 20 20">
          <path d="M10 2L3 7v10l7 5 7-5V7l-7-5z" />
        </svg>
      `
    },
    // B站图标
    BilibiliIcon: {
      template: `
        <svg fill="currentColor" viewBox="0 0 20 20">
          <path d="M2 6a2 2 0 012-2h12a2 2 0 012 2v8a2 2 0 01-2 2H4a2 2 0 01-2-2V6z" />
        </svg>
      `
    },
    // GitHub图标
    GithubIcon: {
      template: `
        <svg fill="currentColor" viewBox="0 0 20 20">
          <path fill-rule="evenodd" d="M10 0C4.477 0 0 4.484 0 10.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0110 4.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.203 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.942.359.31.678.921.678 1.856 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0020 10.017C20 4.484 15.522 0 10 0z" clip-rule="evenodd" />
        </svg>
      `
    }
  }
}
</script>

<style scoped>
/* 页脚基础样式 */
footer {
  background: linear-gradient(135deg, rgba(0, 0, 0, 0.95) 0%, rgba(20, 20, 20, 0.95) 100%);
}

/* 网格布局优化 */
.grid {
  display: grid;
}

.grid-cols-1 {
  grid-template-columns: repeat(1, minmax(0, 1fr));
}

/* 技能标签悬停效果 */
.skill-tag {
  transition: all 0.2s ease;
}

.skill-tag:hover {
  transform: translateY(-1px);
  box-shadow: 0 4px 8px rgba(245, 158, 11, 0.2);
}

/* 联系方式链接悬停效果 */
.contact-link {
  transition: all 0.2s ease;
}

.contact-link:hover {
  transform: translateX(4px);
}

/* 社交媒体图标悬停效果 */
.social-icon {
  transition: all 0.2s ease;
}

.social-icon:hover {
  transform: scale(1.1) rotate(5deg);
}

/* 自定义金色主题类 */
.text-gold-400 {
  color: #FBBF24;
}

.text-gold-500 {
  color: #F59E0B;
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
@media (min-width: 768px) {
  .grid-cols-1 {
    grid-template-columns: repeat(3, minmax(0, 1fr));
  }

  .flex-col {
    flex-direction: row;
  }

  .space-y-4 > :not([hidden]) ~ :not([hidden]) {
    margin-top: 0;
    margin-left: 0;
  }

  .md\:space-y-0 > :not([hidden]) ~ :not([hidden]) {
    margin-top: 0;
  }
}

@media (min-width: 1024px) {
  .max-w-7xl {
    max-width: 1280px;
  }

  .lg\:px-8 {
    padding-left: 2rem;
    padding-right: 2rem;
  }
}

/* 响应式间距 */
.space-x-2 > :not([hidden]) ~ :not([hidden]) {
  margin-left: 0.5rem;
}

.space-x-3 > :not([hidden]) ~ :not([hidden]) {
  margin-left: 0.75rem;
}

.space-x-4 > :not([hidden]) ~ :not([hidden]) {
  margin-left: 1rem;
}

.space-y-3 > :not([hidden]) ~ :not([hidden]) {
  margin-top: 0.75rem;
}

.space-y-4 > :not([hidden]) ~ :not([hidden]) {
  margin-top: 1rem;
}

.gap-2 {
  gap: 0.5rem;
}

.gap-8 {
  gap: 2rem;
}

/* 其他工具类 */
.flex-wrap {
  flex-wrap: wrap;
}

.items-center {
  align-items: center;
}

.justify-between {
  justify-content: space-between;
}

.rounded-full {
  border-radius: 9999px;
}

.rounded-lg {
  border-radius: 0.5rem;
}

.leading-relaxed {
  line-height: 1.625;
}

.mt-auto {
  margin-top: auto;
}

.mb-8 {
  margin-bottom: 2rem;
}

.pt-8 {
  padding-top: 2rem;
}

.py-12 {
  padding-top: 3rem;
  padding-bottom: 3rem;
}

.px-6 {
  padding-left: 1.5rem;
  padding-right: 1.5rem;
}

.px-3 {
  padding-left: 0.75rem;
  padding-right: 0.75rem;
}

.py-1 {
  padding-top: 0.25rem;
  padding-bottom: 0.25rem;
}
</style>
