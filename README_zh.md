# Morphic

一个带生成式 UI 的 AI 聊天应用，基于 [Next.js](https://nextjs.org/)、[Vercel AI SDK](https://sdk.vercel.ai/docs) 和 [OpenAI](https://openai.com/)。

![capture](/public/capture-240404_blk.png)

## 🔍 Overview

- 🧱 [技术栈](#-技术栈)
- 🚀 [快速开始](#-快速开始)
- 🌐 [部署](#-部署)
- ✅ [已验证的模型](#-已验证的模型)

## 🧱 技术栈

- App 框架: [Next.js](https://nextjs.org/)
- 生成式 UI: [Vercel AI SDK](https://sdk.vercel.ai/docs)
- AI 模型: [OpenAI](https://openai.com/)
- 搜索 API: [Tavily AI](https://tavily.com/)
- Headless component primitives: [Radix UI](https://www.radix-ui.com/)
- 组件库: [shadcn/ui](https://ui.shadcn.com/)
- 样式: [Tailwind CSS](https://tailwindcss.com/)

## 🚀 快速开始

### 1. Fork 和 Clone

Fork 项目并克隆到本地。

```
git clone git@github.com:[YOUR_GITHUB_ACCOUNT]/morphic.git
```

### 2. 安装依赖

> kejin 注: Mophic 使用 [Bun](https://bun.sh/) 作为包管理器，如果你没有安装 Bun，请先安装 Bun。

```
cd morphic
bun i
```

### 3. 完善相关秘钥信息

复制一份`.env.local.example`到`.env.local`，并设置你的 OpenAI 和 Tavily API 密钥。

`.env.local`已经被添加到`.gitignore`, 因此不会被提交到 GitHub。请不要直接修改`.env.local.example`文件。

```
cp .env.local.example .env.local
```

你的`.env.local`文件应该包含以下内容:

```
# Used to set the base URL path for OpenAI API requests.
# If you need to set a BASE URL, uncomment and set the following:
# OPENAI_API_BASE=

# Used to set the model for OpenAI API requests.
# If not set, the default is gpt-4-turbo.
# OPENAI_API_MODEL='gpt-4-turbo'

# OpenAI API key retrieved here: https://platform.openai.com/api-keys
OPENAI_API_KEY=[YOUR_OPENAI_API_KEY]

# Tavily API Key retrieved here: https://app.tavily.com/home
TAVILY_API_KEY=[YOUR_TAVILY_API_KEY]
```

**注: 此项目专注于生成式 UI，强依赖于 LLMs 的输出。虽然理论上其他模型也可用，但目前只验证了 OpenAI 官方模型的可用性。我们不保证其他模型的可用性。**

### 4. 本地运行

```
bun dev
```

现在可以访问 http://localhost:3000 查看效果

> kejin 注：启动时间稍微有点长，是正常现象，等启动后再打开网页

## 🌐 部署

可以直接在[Vercel](https://vercel.com/)上部署并在线使用。

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2FKijin-Seija%2Fmorphic&env=OPENAI_API_KEY,TAVILY_API_KEY)

## ✅ 已验证的模型

- [Groq](https://console.groq.com/docs/models)
  - LLaMA3 8b
  - LLaMA3 70b
