# Morphic

一个带生成式 UI 的 AI 聊天应用。

![capture](/public/capture-240404_blk.png)

### Note

此项目和官方网站[morphic.sh](morphic.sh)上的内容有区别。官网的内容在其基础上添加了一些功能，比如权限验证等。方便更好的提供在线服务。不过核心源代码依然是来源于此项目，其代码被设计的更便于部署和开发。使用时请注意区分。

## 🗂️ Overview

- 🛠 [功能](#-功能)
- 🧱 [技术栈](#-技术栈)
- 🚀 [快速开始](#-快速开始)
- 🌐 [部署](#-部署)
- 🔎 [搜索引擎](#-搜索引擎)
- ✅ [已验证的模型](#-已验证的模型)

## 🛠 功能

- 使用生成式 UI 搜索和回答
- 理解用户问题
- 搜索历史
- 分享搜索结果 ([可选](https://github.com/miurla/morphic/blob/main/.env.local.example))
- 支持视频搜索 ([可选](https://github.com/miurla/morphic/blob/main/.env.local.example))
- 从指定 URLs 获取回答
- 作为搜索引擎使用 [※](#-搜索引擎)
- 支持 OpenAI 之外的 AI 提供方
  - Google 生成式 AI [※](https://github.com/miurla/morphic/issues/192)
  - Ollama ([Unstable](https://github.com/miurla/morphic/issues/215))
- 自定义回答模型
  - Groq API [※](https://github.com/miurla/morphic/pull/58)

## 🧱 技术栈

- App 框架: [Next.js](https://nextjs.org/)
- 生成式 UI: [Vercel AI SDK](https://sdk.vercel.ai/docs)
- AI 模型: [OpenAI](https://openai.com/)
- 搜索 API: [Tavily AI](https://tavily.com/) / [Exa AI](https://exa.ai/)
- Serverless 数据库: [Upstash](https://upstash.com/)
- 组件库: [shadcn/ui](https://ui.shadcn.com/)
- Headless component primitives: [Radix UI](https://www.radix-ui.com/)
- 样式: [Tailwind CSS](https://tailwindcss.com/)

## 🚀 快速开始

### 1. Fork 和 Clone

Fork 项目并克隆到本地。

```
git clone git@github.com:[YOUR_GITHUB_ACCOUNT]/morphic.git
```

### 2. 安装依赖

> Kijin 注: Mophic 使用 [Bun](https://bun.sh/) 作为包管理器，如果你没有安装 Bun，请先安装 Bun。

```
cd morphic
bun install
```

### 3. 设置 Upstash Redis

按照下面的指引设置 Upstash Redis，创建一个 Redis database 并获取`UPSTASH_REDIS_REST_URL` 和 `UPSTASH_REDIS_REST_TOKEN`。

参考[Upstash 指引](https://upstash.com/blog/rag-chatbot-upstash#setting-up-upstash-redis)来构建和运行。

> Kijin 注: Upstash 是一个在线 Serverless 服务，提供 Redis, Kafka, QStash 和向量数据库的在线创建和 Rest API 访问。估计是开发者为了提供聊天记录保存而添加的。Upstash 官网: https://upstash.com/

### 4. 完善相关秘钥信息

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

# Upstash Redis URL and Token retrieved here: https://console.upstash.com/redis
UPSTASH_REDIS_REST_URL=
UPSTASH_REDIS_REST_TOKEN=
```

> Kijin 注：相关配置解释<br />
> OPENAI_API_BASE 设置 OpenAI API 请求的基准 URL。如果你需要设置一个 BASE URL，取消注释并设置以下内容：<br />
> OPENAI_API_BASE=<br />
> OPENAI_API_MODEL 设置 OpenAI API 请求的模型。如果未设置，则默认为 gpt-4-turbo。<br />
> OPENAI_API_KEY 设置 OpenAI API 密钥，从 https://platform.openai.com/api-keys 获取。<br />
> TAVILY_API_KEY 设置 Tavily API 密钥，从 https://app.tavily.com/home 获取。<br />
> UPSTASH_REDIS_REST_URL 设置 Upstash Redis URL，从 https://console.upstash.com/redis 获取。<br />
> UPSTASH_REDIS_REST_TOKEN 设置 Upstash Redis Token，从 https://console.upstash.com/redis 获取。

> _以下配置为可选项，请在.env.local.example 中查看。_

> USE_SPECIFIC_API_FOR_WRITER 设置为 true 以使用特定 API 进行编写。它必须与 OpenAI API 兼容。<br />
> SPECIFIC_API_BASE 设置特定 API 的基准 URL。<br />
> SPECIFIC_API_KEY 设置特定 API 的密钥。<br />
> SPECIFIC_API_MODEL 设置特定 API 的模型。<br />

_注: 此项目专注于生成式 UI，强依赖于 LLMs 的输出。虽然理论上其他模型也可用，但目前只验证了 OpenAI 官方模型的可用性。我们不保证其他模型的可用性。_

### 4. 本地运行

```
bun dev
```

现在可以访问 http://localhost:3000 查看效果

> Kijin 注：启动时间可能稍微有点长，是正常现象，等启动后再打开网页

## 🌐 部署

### Vercel

可以直接在[Vercel](https://vercel.com/)上部署并在线使用。

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2FKijin-Seija%2Fmorphic&env=OPENAI_API_BASE,OPENAI_API_KEY,TAVILY_API_KEY,UPSTASH_REDIS_REST_URL,UPSTASH_REDIS_REST_TOKEN)

### Cloudflare Pages

1. Fork 此项目.
2. 创建一个 Cloudflare Pages 项目.
3. 选择 `Morphic` repo 和 `Next.js` preset.
4. 设置 `OPENAI_API_KEY` 和 `TAVILY_API_KEY` 环境变量.
5. 保存并部署.
6. 取消部署, 进入`Settings` -> `Functions` -> `Compatibility flags`, add `nodejs_compat` 进行预览和发布.
7. 重新部署.

**需要解决以下构建问题: [issue](https://github.com/miurla/morphic/issues/114)**

## 🔎 搜索引擎

### 将 Morphic 设置为浏览器的搜索引擎

如果你希望将你的浏览器搜索引擎设置为 Morphic，可以按照以下步骤：

1. 打开浏览器设置
2. 进入“搜索引擎设置”
3. 选择 "管理搜索引擎".
4. 在"搜索网站"下点击“添加”
5. 填入下面的内容:
   - **搜索引擎 e**: Morphic
   - **Shortcut**: morphic
   - **URL with %s in place of query**: `https://morphic.sh/search?q=%s`
6. 点击“添加”保存搜索引擎
7. 在搜索引擎列表里找到 Morphic，点击旁边三点按钮，选择“设为默认”.

这样即可让你的默认搜索引擎变为 Morphic

## ✅ 已验证的模型

### 所有功能都可用的

- OpenAI
  - gpt-4o
  - gpt-4-turbo
  - gpt-3.5-turbo
- Google
  - Gemini 1.5 pro [※](https://github.com/miurla/morphic/issues/192)
- Ollama (Unstable)
  - mistral/openhermes & Phi3/llama3 [※](https://github.com/miurla/morphic/issues/215)

# 已经得到验证的可用于 writers 的模型。

- [Groq](https://console.groq.com/docs/models)
  - LLaMA3 8b
  - LLaMA3 70b
