# 农淑惠作品集网站 - 项目说明文档

## 项目当前状态

**开发阶段**：基础架构和核心组件开发已完成，正在进入页面开发阶段

**环境状态**：

- ✅ Vue 3 + Vite 开发环境已搭建
- ✅ 依赖包已安装并配置完成
- ✅ 开发服务器正常运行（http://localhost:5173/）
- ✅ Tailwind CSS 黑金主题已配置

**技术栈配置完成情况**：

- Vue 3.5.13 (Composition API)
- Vite 6.0.3 (构建工具)
- Vue Router 4.5.0 (路由管理)
- Tailwind CSS 4.0.0 (样式框架)
- PostCSS + Autoprefixer (CSS 处理)
- ESLint (代码规范)

**特殊说明**：

- Tailwind CSS v4.x 采用了新的架构，传统的 `npx tailwindcss init` 命令不再可用
- 项目采用手动配置方式，已成功创建 `tailwind.config.js` 和 `postcss.config.js`
- 黑金主题配色已在全局样式中配置完成

---

## 项目概述

本项目是为广告学专业大学生农淑惠打造的个人作品集网站，主要用于求职面试展示。网站采用现代化的前端技术栈，以艺术创意风格展示多媒体作品，包括平面设计、视频制作、3D 建模等内容。

## 项目目标

- **主要目标**：为面试官提供直观、专业的作品展示平台
- **用户体验**：简洁美观、易于浏览、快速加载
- **技术目标**：使用现代化技术栈，易于维护和更新

## 技术栈规范

### 核心技术

- **前端框架**：Vue 3 (Composition API)
- **构建工具**：Vite
- **路由管理**：Vue Router 4
- **样式框架**：Tailwind CSS
- **状态管理**：无（项目简单，不使用 Vuex/Pinia）

### 开发环境要求

**当前项目环境**：

- Node.js 16+ (项目已验证兼容)
- npm (已使用，版本兼容)
- Windows 10/11 (当前开发环境)
- 现代浏览器（Chrome、Firefox、Safari、Edge）

**快速启动**：

```bash
# 进入项目目录
cd c:\Users\34682\Desktop\portfolio-vue

# 安装依赖（如果尚未安装）
npm install

# 启动开发服务器
npm run dev

# 访问地址：http://localhost:5173/
```

**构建命令**：

```bash
# 构建生产版本
npm run build

# 预览构建结果
npm run preview

# 代码检查
npm run lint
```

## 设计规范

### 视觉风格

- **主题色彩**：黑金配色方案
  - 主色：深黑色 (#000000, #1a1a1a)
  - 辅助色：金色 (#FFD700, #FFA500)
  - 背景色：深灰色 (#2d2d2d, #3a3a3a)
- **字体**：现代无衬线字体，确保可读性
- **风格定位**：艺术创意、专业简约、视觉冲击力强

### 布局规范

- **布局方式**：网格布局 + 卡片式设计
- **响应式**：主要适配 PC 端（1920x1080、1366x768）
- **导航**：顶部固定导航栏
- **内容区域**：居中对齐，最大宽度限制

## 功能规范

### 基础功能（必须实现）

1. **多页面导航**

   - 首页（个人介绍）
   - 作品展示页（分类展示）
   - 关于我页面

2. **媒体展示**

   - 图片展示：支持点击放大查看
   - 视频播放：内嵌播放器，支持常见格式
   - 图片懒加载：优化页面加载速度

3. **作品分类**
   - MG 动画作品
   - PR 剪辑作品
   - 平面设计作品
   - C4D 建模作品
   - 项目经验展示

### 进阶功能（可选实现）

1. **联系表单**：简单的联系方式表单
2. **主题切换**：黑金主题的深浅模式切换
3. **作品筛选**：按类别筛选作品

## 文件结构规范

**当前项目结构**：

```
portfolio-vue/
├── .editorconfig         # 编辑器配置
├── .gitattributes        # Git 属性配置
├── .gitignore           # Git 忽略文件
├── .vscode/             # VS Code 配置
│   ├── extensions.json  # 推荐扩展
│   └── settings.json    # 编辑器设置
├── public/              # 静态资源
│   ├── favicon.ico      # 网站图标
│   └── 农淑惠作品集/      # 原始作品资源文件夹 ✅
│       ├── 1.MG动画/
│       ├── 2.PR剪辑/
│       ├── 3.平面设计/
│       ├── 4.C4D建模/
│       └── 项目经验/
├── src/                 # 源代码 ✅
│   ├── components/      # 可复用组件
│   │   ├── MainLayout.vue    # 主布局组件 ✅
│   │   ├── NavBar.vue        # 导航栏组件 ✅
│   │   ├── Footer.vue        # 页脚组件 ✅
│   │   ├── PageContainer.vue # 页面容器组件 ✅
│   │   ├── WorkCard.vue      # 作品卡片组件 ✅
│   │   ├── ImageViewer.vue   # 图片查看器组件 ✅
│   │   ├── VideoPlayer.vue   # 视频播放器组件 ✅
│   │   ├── LoadingSpinner.vue # 加载动画组件 ✅
│   │   ├── HelloWorld.vue    # 默认组件（待移除）
│   │   ├── TheWelcome.vue    # 欢迎组件（待移除）
│   │   ├── WelcomeItem.vue   # 欢迎项组件（待移除）
│   │   └── icons/           # 图标组件
│   ├── views/          # 页面组件
│   │   ├── AboutView.vue    # 关于页面
│   │   └── HomeView.vue     # 首页
│   ├── router/         # 路由配置 ✅
│   │   └── index.js    # 路由配置文件
│   ├── assets/         # 项目资源 ✅
│   │   ├── base.css    # 基础样式
│   │   ├── main.css    # 主样式文件（已配置黑金主题）
│   │   └── logo.svg    # Logo 文件
│   ├── App.vue         # 根组件 ✅
│   └── main.js         # 入口文件 ✅
├── eslint.config.js     # ESLint 配置 ✅
├── index.html          # HTML 模板 ✅
├── jsconfig.json       # JavaScript 配置 ✅
├── package.json        # 项目配置 ✅
├── package-lock.json   # 依赖锁定文件 ✅
├── postcss.config.js   # PostCSS 配置 ✅
├── tailwind.config.js  # Tailwind 配置 ✅
├── vite.config.js      # Vite 配置 ✅
├── 开发计划.md          # 开发计划文档 ✅
└── README.md           # 项目说明 ✅
```

**说明**：

- ✅ 标记表示已存在并配置完成
- 原始作品文件已移回 `public/农淑惠作品集/` 目录
- 项目基础架构和核心组件已完整搭建
- 布局组件和通用组件开发已完成
- 下一步将开发页面组件（HomePage、PortfolioPage、AboutPage）

## 代码规范

### Vue 组件规范

- 使用 Composition API
- 组件名采用 PascalCase
- 文件名采用 kebab-case
- 必须添加适当的注释

### CSS 规范

- 优先使用 Tailwind CSS 类
- 自定义样式使用 CSS Modules 或 scoped
- 遵循 BEM 命名规范（如需自定义类名）

### 代码质量

- 保持代码简洁易读
- 适当添加错误处理
- 确保组件可复用性

#### 组件开发最佳实践

**组件命名规范**：

- 避免使用 HTML 保留名称（如 `Footer`），推荐使用多词组合（如 `AppFooter`）
- 组件名采用 PascalCase，文件名采用 kebab-case
- 确保组件名称语义化，便于理解和维护

**样式优化建议**：

- 避免使用不存在的 Tailwind CSS 类（如 `text-gold-400`）
- 优先使用标准 CSS 属性而非 `@apply` 指令，提高兼容性
- 使用 CSS 变量统一管理主题色彩，便于全局调整
- 移除空的 CSS 规则集，保持代码整洁

**代码结构优化**：

- 将配置数据外部化，使用独立的配置文件管理
- 对于非响应式数据，使用 `shallowRef` 优化性能
- 合理使用 Vue 3 Composition API，提高代码可读性
- 添加适当的 TypeScript 类型定义（可选）

**可访问性改进**：

- 为交互元素添加 ARIA 标签
- 确保键盘导航支持
- 提供合适的焦点指示器
- 使用语义化 HTML 标签

#### 已完成组件列表

**布局组件**：

- `MainLayout` - 主布局组件，提供页面整体结构
- `NavBar` - 导航栏组件，包含路由导航和 Logo
- `Footer` - 页脚组件，展示个人信息和联系方式
- `PageContainer` - 页面容器组件，提供统一的页面布局

**通用组件**：

- `WorkCard` - 作品卡片组件，支持多种布局模式
- `ImageViewer` - 图片查看器组件，支持放大、缩放和导航
- `VideoPlayer` - 视频播放器组件，自定义播放控制
- `LoadingSpinner` - 加载动画组件，多种动画效果

#### 组件使用示例

**MainLayout 主布局组件**：

```vue
<!-- 基础使用 -->
<template>
  <MainLayout>
    <template #header>
      <NavBar />
    </template>

    <template #main>
      <PageContainer title="首页" subtitle="欢迎来到我的作品集">
        <!-- 页面内容 -->
      </PageContainer>
    </template>

    <template #footer>
      <AppFooter />
    </template>
  </MainLayout>
</template>

<script>
import MainLayout from "@/components/MainLayout.vue";
import NavBar from "@/components/NavBar.vue";
import AppFooter from "@/components/Footer.vue";
import PageContainer from "@/components/PageContainer.vue";

export default {
  components: {
    MainLayout,
    NavBar,
    AppFooter,
    PageContainer,
  },
};
</script>
```

**NavBar 导航栏组件**：

```vue
<!-- 在页面中使用导航栏 -->
<template>
  <NavBar />
</template>

<script>
import NavBar from "@/components/NavBar.vue";

export default {
  components: {
    NavBar,
  },
};
</script>
```

**AppFooter 页脚组件**：

```vue
<!-- 在页面中使用页脚 -->
<template>
  <AppFooter />
</template>

<script>
import AppFooter from "@/components/Footer.vue";

export default {
  components: {
    AppFooter,
  },
};
</script>
```

**PageContainer 页面容器组件**：

```vue
<!-- 基础使用 -->
<template>
  <PageContainer title="作品展示" subtitle="我的创意作品集合">
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <!-- 作品内容 -->
    </div>
  </PageContainer>
</template>

<!-- 高级配置 -->
<template>
  <PageContainer
    title="关于我"
    subtitle="了解更多关于我的信息"
    :show-header="true"
    :show-footer="true"
    max-width="4xl"
    padding="lg"
    :fullscreen="false"
    background="gradient"
  >
    <div class="prose prose-invert max-w-none">
      <!-- 页面内容 -->
    </div>

    <template #footer>
      <div class="text-center text-gray-400 text-sm">最后更新：2024年12月</div>
    </template>
  </PageContainer>
</template>

<script>
import PageContainer from "@/components/PageContainer.vue";

export default {
  components: {
    PageContainer,
  },
};
</script>
```

**完整页面示例**：

```vue
<!-- views/HomePage.vue -->
<template>
  <MainLayout>
    <template #header>
      <NavBar />
    </template>

    <template #main>
      <PageContainer
        title="农淑惠"
        subtitle="广告学专业 | 创意设计师"
        background="gradient"
      >
        <!-- 个人介绍区域 -->
        <section class="mb-16">
          <div class="text-center">
            <img
              src="/avatar.jpg"
              alt="农淑惠"
              class="w-32 h-32 rounded-full mx-auto mb-6 border-4 border-gold-500"
            />
            <p class="text-lg text-gray-300 max-w-2xl mx-auto">
              专注于MG动画、视频剪辑和平面设计的创意工作者，
              致力于用视觉艺术传达美好故事。
            </p>
          </div>
        </section>

        <!-- 特色作品展示 -->
        <section>
          <h2 class="text-2xl font-bold text-white mb-8 text-center">
            特色作品
          </h2>
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            <WorkCard
              v-for="work in featuredWorks"
              :key="work.id"
              :work="work"
              layout="card"
              @click="openWork"
            />
          </div>
        </section>
      </PageContainer>
    </template>

    <template #footer>
      <AppFooter />
    </template>
  </MainLayout>
</template>

<script>
import MainLayout from "@/components/MainLayout.vue";
import NavBar from "@/components/NavBar.vue";
import AppFooter from "@/components/Footer.vue";
import PageContainer from "@/components/PageContainer.vue";

export default {
  name: "HomePage",
  components: {
    MainLayout,
    NavBar,
    AppFooter,
    PageContainer,
  },
};
</script>
```

## 性能优化规范

### 图片优化

- 使用适当的图片格式（WebP 优先，JPEG/PNG 备选）
- 实现图片懒加载
- 压缩图片大小，保持质量平衡

### 代码优化

- 组件按需加载
- 避免不必要的重渲染
- 合理使用 Vue 的响应式特性

## 部署规范

### 部署平台

- **推荐平台**：Netlify
- **部署方式**：Git 自动部署
- **域名**：使用 Netlify 提供的免费域名

### 构建配置

- 生产环境构建命令：`npm run build`
- 输出目录：`dist/`
- 确保所有资源路径正确

## 维护更新规范

### 内容更新

- 作品文件统一放在 `农淑惠作品集/` 目录
- 新增作品需要更新对应的数据配置
- 定期检查链接和媒体文件的有效性

### 代码维护

- 保持依赖包的更新
- 定期备份项目代码
- 记录重要的修改和更新

## 学习目标

通过本项目，用户应该掌握：

1. Vue 3 基础语法和 Composition API
2. Vite 构建工具的使用
3. Tailwind CSS 的应用
4. 前端项目的部署流程
5. 基础的项目维护和更新方法

## 注意事项

1. **简单优先**：避免过度复杂的功能和动画
2. **性能考虑**：确保网站加载速度
3. **兼容性**：主要考虑现代浏览器
4. **可维护性**：代码结构清晰，便于后续修改
5. **用户体验**：以展示作品为核心，避免干扰元素

---

_本文档将随着项目开发进度持续更新和完善_
