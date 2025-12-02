# Netlify 部署指南

## 🔧 已修复的问题

### 1. API Key 错误 ✅
**问题**: `Uncaught Error: An API Key must be set when running in a browser`
**原因**: Vite 环境变量配置不完整
**解决**: 
- 更新了 `vite.config.ts` 正确加载和注入环境变量
- 确保 `GEMINI_API_KEY` 在构建时被正确替换

### 2. Tailwind CSS CDN 警告 ✅
**问题**: `cdn.tailwindcss.com should not be used in production`
**原因**: 使用 CDN 版本而非构建版本
**解决**:
- 安装了 `tailwindcss`, `postcss`, `autoprefixer` 为项目依赖
- 创建了 `tailwind.config.js` 和 `postcss.config.js`
- 移除了 HTML 中的 CDN 引用
- 创建了 `index.css` 文件导入 Tailwind

### 3. mise.toml 错误 ✅
**原因**: Netlify 环境中没有 `mise` 命令
**解决**: 已配置 `netlify.toml` 来忽略此工具

### 4. MaxListenersExceededWarning ⚠️
**状态**: 这是**无害的警告**，不影响生产部署
**原因**: Netlify dev server 和 Vite 同时运行时的正常行为

## 🚀 部署步骤

### 0. 重新安装依赖（重要！）

在本地运行以下命令安装新的依赖（Tailwind CSS）：

```bash
npm install
```

### 1. 在 Netlify 控制台配置环境变量

**这是最关键的步骤！**

进入 Netlify 网站设置页面：
- Site settings → Environment variables
- 点击 "Add a variable" 或 "Add environment variable"
- 添加以下变量：
  - **Key**: `GEMINI_API_KEY`
  - **Value**: 您的 Google AI Studio API 密钥（从 [Google AI Studio](https://aistudio.google.com/apikey) 获取）
- 点击 "Save"

⚠️ **注意**: 如果没有正确设置此环境变量，会出现 "An API Key must be set when running in a browser" 错误！

### 2. 部署配置

项目已包含以下配置文件：

- ✅ `netlify.toml` - Netlify 构建配置
- ✅ `.nvmrc` - Node 版本配置 (v18)
- ✅ `public/_redirects` - SPA 路由重定向
- ✅ `.env.example` - 环境变量示例

### 3. 部署方式

#### 方式 A：通过 Git 连接部署（推荐）
1. 将代码推送到 GitHub/GitLab/Bitbucket
2. 在 Netlify 中导入项目
3. Netlify 会自动检测配置并部署

#### 方式 B：手动部署
1. 本地运行 `npm run build`
2. 将 `dist` 文件夹拖拽到 Netlify 部署页面

## 构建配置说明

```toml
[build]
  command = "npm run build"    # 构建命令
  publish = "dist"              # 发布目录

[build.environment]
  NODE_VERSION = "18"           # Node 版本
  NODE_OPTIONS = "--max-old-space-size=4096"  # 内存限制
```

## 常见问题解决

### Q1: 看到 "mise: command not found" 错误
**A**: 这个错误可以忽略。`netlify.toml` 已配置为跳过 mise 工具检查。

### Q2: MaxListenersExceededWarning 警告
**A**: 这是 Netlify dev server 的正常行为，不影响生产环境。可以忽略。

### Q3: 部署后页面刷新显示 404
**A**: 已通过 `_redirects` 文件和 `netlify.toml` 配置解决。

### Q4: 环境变量未生效
**A**: 确保在 Netlify 控制台正确设置了 `GEMINI_API_KEY`。

## 验证部署

部署成功后：
1. 访问 Netlify 提供的 URL
2. 测试应用功能
3. 检查浏览器控制台是否有 API 相关错误

## 本地测试 Netlify 构建

安装 Netlify CLI：
```bash
npm install -g netlify-cli
```

测试构建：
```bash
netlify build
```

本地运行 Netlify dev server：
```bash
netlify dev
```

## 支持

如遇到其他问题：
1. 检查 Netlify 部署日志
2. 验证环境变量配置
3. 确认 Node 版本为 18 或更高
