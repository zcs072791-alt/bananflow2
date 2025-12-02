<div align="center">
<img width="1200" height="475" alt="GHBanner" src="https://github.com/user-attachments/assets/0aa67016-6eaf-458a-adb2-6e31a0763ed6" />
</div>

# Run and deploy your AI Studio app

This contains everything you need to run your app locally.

View your app in AI Studio: https://ai.studio/apps/drive/1NbvpK69Erm5DpucMWZCe3ryEPQ9lYP47

## Run Locally

**Prerequisites:**  Node.js 18+

### First Time Setup

1. **Install dependencies**:
   ```bash
   npm install
   ```

2. **Set up environment variables**:
   - Copy `.env.example` to `.env.local`
   - Add your Gemini API key:
     ```
     GEMINI_API_KEY=your_api_key_here
     ```

3. **Run the app**:
   ```bash
   npm run dev
   ```
   
   App will be available at: http://localhost:3000

## Deploy to Netlify

### ⚠️ 重要：部署前请先更新依赖

如果您之前已经克隆了此项目，请先运行：
```bash
npm install
```

### 部署步骤

1. **配置环境变量 (关键步骤！)**
   - 登录 Netlify 控制台
   - 进入：Site settings → Environment variables
   - 添加环境变量：
     - Key: `GEMINI_API_KEY`
     - Value: 您的 Google AI Studio API 密钥
   - 📌 获取 API Key: https://aistudio.google.com/apikey

2. **部署项目**
   - 方式 A（推荐）：连接 GitHub/GitLab 仓库到 Netlify
   - 方式 B：使用 Netlify CLI: `netlify deploy --prod`
   - 构建设置已在 `netlify.toml` 中配置

3. **验证部署**
   - 访问部署的 URL
   - 打开浏览器控制台，确认没有 API Key 错误
   - 测试应用功能

### 常见问题

- ❌ **Error: An API Key must be set** → 检查 Netlify 环境变量是否正确设置
- ⚠️ **Tailwind CDN 警告** → 已修复，现使用构建版本
- ⚠️ **MaxListenersExceededWarning** → 无害警告，可忽略

📖 详细部署指南请查看 [NETLIFY_DEPLOYMENT.md](./NETLIFY_DEPLOYMENT.md)
