# iLLMHub 用户手册

> **iLLMHub** 是全球领先的大模型 API 服务平台,聚合 Claude、OpenAI、Gemini、DeepSeek 等主流模型 API,统一接入、按量计费。

---

## 目录

1. [平台简介](#1-平台简介)
2. [快速开始](#2-快速开始)
3. [注册与登录](#3-注册与登录)
4. [套餐与充值](#4-套餐与充值)
5. [获取 API Key](#5-获取-api-key)
6. [API 端点说明](#6-api-端点说明)
7. [各工具配置教程](#7-各工具配置教程)
8. [支持的模型列表](#8-支持的模型列表)
9. [常见问题 (FAQ)](#9-常见问题-faq)
10. [技术支持](#10-技术支持)
11. [术语表](#11-术语表)
12. [快速参考卡](#12-快速参考卡)
13. [最佳实践](#13-最佳实践)
14. [故障排查流程图](#14-故障排查流程图)

---

## 1. 平台简介

**iLLMHub** 是一个全球领先的大模型 API 服务平台,将 Claude、OpenAI、Gemini、DeepSeek 等多家 AI 产品的 API 汇聚至一个统一入口。

### 核心特点

- **统一接口** - 兼容 OpenAI 和 Anthropic 两种 API 格式,一套代码对接多家模型
- **稳定可靠** - 主备双端点保障,国内网络友好
- **按量计费** - 按 Token 用量扣费,用多少付多少
- **主流模型全覆盖** - Claude、GPT、Gemini、DeepSeek 等一站式接入

### 适用场景

- 开发者在 Claude Code、Cursor、Trae 等编程工具中使用 AI 辅助编码
- 通过 Python/Node.js/curl 等调用 AI API 进行应用开发
- 团队共享 AI 订阅额度,降低成本

---

## 2. 快速开始

> **本章导读**:想在 5 分钟内完成第一次 API 调用?跟着本章操作,从注册到调用成功只需 5 步!

### 2.1 第一步:注册账号

1. 访问 **https://illmhub.ai**
2. 点击 **注册**
3. 填写邮箱和密码
4. 完成邮箱验证

> 💡 **零基础提示**:注册只需 1 分钟,邮箱验证邮件可能在垃圾邮件中。

### 2.2 第二步:充值

1. 登录后进入 **充值** 页面
2. 选择金额(建议先小额充值测试)
3. 使用支付宝/微信扫码支付
4. 余额实时到账

### 2.3 第三步:获取 API Key

1. 进入 **API Key 管理**
2. 点击 **创建新 Key**
3. 复制并保存 Key(格式:`sk-xxxx...xxxx`)

> ⚠️ **重要**:Key 只显示一次!立即复制保存。

### 2.4 第四步:配置工具

以 **Claude Code** 为例:

```bash
# 设置环境变量
export ANTHROPIC_BASE_URL=https://api.illm.io
export ANTHROPIC_API_KEY=<你复制的Key>

# 持久化(添加到 ~/.zshrc)
echo 'export ANTHROPIC_BASE_URL=https://api.illm.io' >> ~/.zshrc
echo 'export ANTHROPIC_API_KEY=<你复制的Key>' >> ~/.zshrc
source ~/.zshrc
```

### 2.5 第五步:测试调用

**方式一:使用 Claude Code**

```bash
# 启动 Claude Code
claude

# 输入测试消息
你好,请介绍一下自己
```

**方式二:使用 Python**

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://api.illm.io/v1",
    api_key="***"
)

response = client.chat.completions.create(
    model="gpt-5",
    messages=[{"role": "user", "content": "你好"}]
)

print(response.choices[0].message.content)
```

**方式三:使用 curl**

```bash
curl https://api.illm.io/v1/chat/completions \
  -H "Authorization: Bearer ***" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-5",
    "messages": [{"role": "user", "content": "你好"}]
  }'
```

### 2.6 常见问题

**Q: 连接失败?**
- 检查网络
- 尝试备用端点:`https://api.illm.my`

**Q: 认证失败?**
- 检查 Key 是否正确
- 确认 Key 没有被禁用

> 💡 余额问题、网络代理等更多问题请见 [第 9 章:常见问题 (FAQ)](#9-常见问题-faq)。

---

> 🎉 **恭喜!** 你已完成第一次 API 调用!接下来可以:
>
> - 阅读 [第 6 章:API 端点说明](#6-api-端点说明) 了解详细参数
> - 阅读 [第 7 章:各工具配置教程](#7-各工具配置教程) 配置其他工具
> - 阅读 [第 8 章:支持的模型列表](#8-支持的模型列表) 选择合适的模型

> 📷 **[截图占位:iLLMHub 平台主界面截图]** - 展示平台首页和导航栏
> 📷 **[截图占位:API Key 获取流程截图]** - 展示从登录到获取 API Key 的完整步骤

---

## 3. 注册与登录

### 3.1 注册账号

1. 访问 iLLMHub 官网:**https://illmhub.ai**
2. 点击页面上的 **注册** 按钮
3. 填写邮箱地址和密码
4. 完成邮箱验证(查收验证邮件并点击链接)
5. 注册成功,自动跳转到用户后台

### 3.2 登录

1. 访问 **https://illmhub.ai**
2. 点击 **登录**
3. 输入注册时的邮箱和密码
4. 进入用户后台(Dashboard)

> 💡 **提示**:登录后可以在后台查看余额、管理 API Key、查看用量统计等。

> 📷 **[截图占位:注册页面截图]** - 展示注册表单和填写示例
> 📷 **[截图占位:登录页面截图]** - 展示登录入口和第三方登录选项

---

## 4. 套餐与充值

### 4.1 充值流程

1. 登录后台,进入 **充值** 或 **套餐** 页面
2. 选择充值金额或套餐
3. 选择支付方式完成支付
4. 余额实时到账

### 4.2 支持的支付方式

iLLMHub 内置支付系统,支持以下支付方式:

| 支付方式 | 说明 |
|---------|------|
| **支付宝** | 扫码支付 |
| **微信支付** | 扫码支付 |
| **Stripe** | 国际信用卡(Visa/Mastercard) |

> 具体支持的支付方式以平台后台实际显示为准;若有出入,以 [第 10 章:技术支持](#10-技术支持) 为准。

### 4.3 计费说明

- **按 Token 计费**:根据实际使用的 Token 数量扣费
- **不同模型不同倍率**:各模型的输入/输出 Token 单价不同,具体费率以平台后台实际显示为准;若有出入,以 [第 10 章:技术支持](#10-技术支持) 为准
- **余额查询**:登录后台首页即可查看当前余额和用量统计

> 📷 **[截图占位:套餐选择页面截图]** - 展示各套餐选项、价格和支付方式

---

## 5. 获取 API Key

API Key 是调用 iLLMHub API 的凭证,每个用户可以创建多个 Key。

### 5.1 创建 API Key

1. 登录后台
2. 进入 **API Key 管理** 页面
3. 点击 **创建新 Key**
4. 为 Key 设置一个备注名称(如"开发测试"、"生产环境")
5. 点击确认,系统会生成一个新的 API Key

### 5.2 保存 API Key

> ⚠️ **重要**:API Key 只会显示一次!创建后请立即复制并妥善保存。如果丢失,需要重新创建新的 Key。

API Key 格式通常为 `sk-xxxx...xxxx`,请将其保存在安全的地方,不要泄露给他人或提交到公开代码仓库。

> 📷 **[截图占位:API Key 管理页面截图]** - 展示创建、查看、删除 API Key 的操作界面

## 6. API 端点说明

> **本章导读**:本章将详细介绍 iLLMHub 的 API 端点配置,包括主端点与备用端点的区别、OpenAI 和 Anthropic 两种兼容格式的使用方法、各种请求参数的详细解释,以及完整的代码示例。读完本章后,你将能够根据自己的需求选择合适的端点和 API 格式。

---

## 6.1 主端点与备用端点

### 6.1.1 端点地址

iLLMHub 提供两个 API 端点:

| 端点 | 地址 | 说明 |
|------|------|------|
| **主端点** | `https://api.illm.io` | 推荐使用,性能最优 |
| **备用端点** | `https://api.illm.my` | 主端点不可用时切换 |

> 💡 **零基础提示**:两个端点的功能完全一样,只是网络线路不同。就像同一个店铺有两个门,从哪个门进都能买到东西。

### 6.1.2 如何选择端点

**选择建议**:

```text
如果你在国内:
  先试 api.illm.my(备用端点,国内优化)
  如果不行,再试 api.illm.io(主端点)

如果你在海外:
  优先用 api.illm.io(主端点)
  如果不行,再试 api.illm.my(备用端点)
```

**为什么有两个端点?**

- 网络环境复杂,有时候某个域名可能被临时限制
- 两个端点部署在不同服务器,提高可用性
- 国内用户使用备用端点通常更稳定

> ⚠️ **注意**:两个端点的 API Key 是通用的,你不需要为不同端点创建不同的 Key。

### 6.1.3 端点切换方法

**方法一:修改环境变量**

```bash
# 使用主端点
export OPENAI_BASE_URL=https://api.illm.io/v1

# 切换到备用端点
export OPENAI_BASE_URL=https://api.illm.my/v1
```

**方法二:修改配置文件**

```json
{
  "models": {
    "providers": {
      "illmhub": {
        "baseUrl": "https://api.illm.my/v1"
      }
    }
  }
}
```

**方法三:代码中直接指定**

```python
from openai import OpenAI

# 使用主端点
client = OpenAI(
    base_url="https://api.illm.io/v1",
    api_key="***"
)

# 切换到备用端点
client = OpenAI(
    base_url="https://api.illm.my/v1",
    api_key="***"
)
```

---

## 6.2 OpenAI 兼容格式

### 6.2.1 基本信息

| 项目 | 说明 |
|------|------|
| **端点路径** | `/v1/chat/completions` |
| **请求方法** | `POST` |
| **Content-Type** | `application/json` |
| **认证方式** | `Authorization: Bearer <API Key>` |

**适用模型**:GPT-5 / GPT-5.5、GPT-5-mini / nano、GPT-5.3-Codex、Gemini 3 / 3.1 / 3.5 Flash、DeepSeek V3.2 / V4、Claude 系列(推荐格式)

> 💡 **API 进化说明**:
> - OpenAI 已推出新一代 **Responses API**(集成 web search、file search、computer use 等能力),官方推荐新项目使用。
> - 但 OpenAI 明确表示 **Chat Completions API 将 indefinitely 支持**,iLLMHub 当前默认走该路径,代码零迁移。
> - ⚠️ **OpenAI Assistants API 将于 2026-08-26 关闭**,如仍在使用请迁移。

### 6.2.2 请求参数详解

**完整请求示例**:

```json
{
  "model": "gpt-5",
  "messages": [
    {
      "role": "system",
      "content": "你是一个有帮助的助手"
    },
    {
      "role": "user",
      "content": "你好"
    }
  ],
  "stream": false,
  "temperature": 0.7,
  "max_tokens": 1024,
  "top_p": 1.0,
  "frequency_penalty": 0,
  "presence_penalty": 0
}
```

**参数说明**:

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `model` | string | ✅ | 模型名称,如 `gpt-5`、`claude-sonnet-4-6` |
| `messages` | array | ✅ | 消息数组,包含对话历史 |
| `stream` | boolean | ❌ | 是否流式输出,默认 `false` |
| `temperature` | float | ❌ | 生成随机性,0-2,默认 1.0。值越大越随机 |
| `max_tokens` | integer | ❌ | 最大输出 Token 数 |
| `top_p` | float | ❌ | 核采样参数,0-1,默认 1.0 |
| `frequency_penalty` | float | ❌ | 频率惩罚,-2 到 2,默认 0 |
| `presence_penalty` | float | ❌ | 存在惩罚,-2 到 2,默认 0 |

**messages 数组结构**:

```json
{
  "messages": [
    {"role": "system", "content": "系统提示词"},
    {"role": "user", "content": "用户消息"},
    {"role": "assistant", "content": "AI回复"},
    {"role": "user", "content": "用户新消息"}
  ]
}
```

| role | 说明 |
|------|------|
| `system` | 系统提示词,设定 AI 的行为(可选) |
| `user` | 用户消息 |
| `assistant` | AI 的回复(用于多轮对话) |

> 💡 **零基础提示**:`temperature` 参数控制 AI 回复的随机性。如果你想要更稳定的回复,设置为 0.1-0.3;如果想要更有创意的回复,设置为 0.7-1.0。

### 6.2.3 响应格式

**非流式响应**:

```json
{
  "id": "chatcmpl-xxx",
  "object": "chat.completion",
  "created": 1716368000,
  "model": "gpt-5",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "你好!有什么可以帮助你的吗?"
      },
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 10,
    "completion_tokens": 20,
    "total_tokens": 30
  }
}
```

**响应字段说明**:

| 字段 | 说明 |
|------|------|
| `id` | 请求唯一标识 |
| `model` | 实际使用的模型 |
| `choices[0].message.content` | AI 的回复内容 |
| `choices[0].finish_reason` | 结束原因:`stop`(正常)、`length`(达到 max_tokens) |
| `usage` | Token 使用统计 |

**流式响应**:

```json
{"id":"chatcmpl-xxx","choices":[{"index":0,"delta":{"role":"assistant","content":"你"},"finish_reason":null}]}
{"id":"chatcmpl-xxx","choices":[{"index":0,"delta":{"content":"好"},"finish_reason":null}]}
{"id":"chatcmpl-xxx","choices":[{"index":0,"delta":{"content":"!"},"finish_reason":null}]}
{"id":"chatcmpl-xxx","choices":[{"index":0,"delta":{},"finish_reason":"stop"}]}
```

> 💡 **零基础提示**:流式响应是多个 JSON 对象,每个对象包含一小段文本。你需要拼接这些文本才能得到完整的回复。

---

## 6.3 Anthropic 兼容格式

### 6.3.1 基本信息

| 项目 | 说明 |
|------|------|
| **端点路径** | `/v1/messages` |
| **请求方法** | `POST` |
| **Content-Type** | `application/json` |
| **认证方式** | `x-api-key: <API Key>` |

**适用模型**:Claude Fable 5(顶级)、Claude Mythos 5(限定)、Claude Sonnet 4.6/4.5/4.7、Claude Opus 4.6/4.7/4.8、Claude Haiku 4.5

### 6.3.2 请求参数详解

**完整请求示例**:

```json
{
  "model": "claude-sonnet-4-6",
  "max_tokens": 1024,
  "system": "你是一个有帮助的助手",
  "messages": [
    {
      "role": "user",
      "content": "你好"
    }
  ],
  "stream": false,
  "temperature": 0.7
}
```

**参数说明**:

| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `model` | string | ✅ | Claude 模型名称 |
| `max_tokens` | integer | ✅ | 最大输出 Token 数(Claude 必填) |
| `messages` | array | ✅ | 消息数组 |
| `system` | string | ❌ | 系统提示词(独立于 messages) |
| `stream` | boolean | ❌ | 是否流式输出,默认 `false` |
| `temperature` | float | ❌ | 生成随机性,0-1,默认 1.0 |

> ⚠️ **注意**:Anthropic 格式的 `system` 参数是顶级字段,不在 `messages` 数组中。这与 OpenAI 格式不同。

### 6.3.3 响应格式

**非流式响应**:

```json
{
  "id": "msg_xxx",
  "type": "message",
  "role": "assistant",
  "content": [
    {
      "type": "text",
      "text": "你好!有什么可以帮助你的吗?"
    }
  ],
  "model": "claude-sonnet-4-6",
  "stop_reason": "end_turn",
  "usage": {
    "input_tokens": 10,
    "output_tokens": 20
  }
}
```

**响应字段说明**:

| 字段 | 说明 |
|------|------|
| `id` | 消息唯一标识 |
| `content[0].text` | AI 的回复内容 |
| `stop_reason` | 结束原因:`end_turn`(正常)、`max_tokens`(达到限制) |
| `usage` | Token 使用统计 |

---

## 6.4 错误码说明

### 6.4.1 常见错误码

| 错误码 | 说明 | 解决方案 |
|--------|------|---------|
| **401** | 认证失败 | 检查 API Key 是否正确 |
| **403** | 无权限 | 检查 Key 是否被禁用或模型是否可用 |
| **404** | 端点不存在 | 检查 URL 路径是否正确 |
| **429** | 请求过于频繁 | 降低请求频率或联系客服提升限额 |
| **500** | 服务器内部错误 | 稍后重试或切换端点 |
| **502** | 网关错误 | 稍后重试或切换端点 |
| **503** | 服务不可用 | 稍后重试或切换端点 |

### 6.4.2 错误响应格式

**OpenAI 格式错误**:

```json
{
  "error": {
    "message": "Invalid API key",
    "type": "invalid_request_error",
    "code": "invalid_api_key"
  }
}
```

**Anthropic 格式错误**:

```json
{
  "type": "error",
  "error": {
    "type": "authentication_error",
    "message": "Invalid API key"
  }
}
```

### 6.4.3 错误处理最佳实践

```python
import openai
from openai import OpenAI

# 初始化 OpenAI 客户端
client = OpenAI(
    base_url="https://api.illm.io/v1",
    api_key="***"
)

try:
    # 尝试调用 API
    response = client.chat.completions.create(
        model="gpt-5",
        messages=[{"role": "user", "content": "你好"}]
    )
    print(response.choices[0].message.content)
except openai.AuthenticationError:
    # API Key 无效
    print("API Key 无效,请检查 Key 是否正确")
except openai.RateLimitError:
    # 请求过于频繁
    print("请求过于频繁,请稍后重试")
except openai.APIError as e:
    # 其他 API 错误
    print(f"API 错误: {e}")
except Exception as e:
    # 未知错误
    print(f"未知错误: {e}")
```

---

## 6.5 代码示例

### 6.5.1 Python 示例

**示例 1:基本对话**

```python
from openai import OpenAI

# 初始化 OpenAI 客户端,指向 iLLMHub 端点
client = OpenAI(
    base_url="https://api.illm.io/v1",  # iLLMHub 主端点
    api_key="***"                        # 你的 API Key
)

# 创建对话请求
response = client.chat.completions.create(
    model="gpt-5",  # 使用 GPT-5 模型
    messages=[{"role": "user", "content": "你好,请介绍一下自己"}]
)

# 输出 AI 回复
print(response.choices[0].message.content)
```

**示例 2:流式输出**

```python
from openai import OpenAI

# 初始化 OpenAI 客户端
client = OpenAI(
    base_url="https://api.illm.io/v1",
    api_key="***"
)

# 创建流式请求,stream=True 启用流式输出
stream = client.chat.completions.create(
    model="gpt-5",
    messages=[{"role": "user", "content": "写一首关于春天的诗"}],
    stream=True
)

# 逐块接收并输出内容
for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="")
```

**示例 3:多轮对话**

```python
from openai import OpenAI

# 初始化 OpenAI 客户端
client = OpenAI(
    base_url="https://api.illm.io/v1",
    api_key="***"
)

# 初始化对话历史,包含系统提示词
messages = [
    {"role": "system", "content": "你是一个友好的助手"},
    {"role": "user", "content": "我叫小明"}
]

# 第一轮对话
response = client.chat.completions.create(
    model="gpt-5",
    messages=messages
)
print(response.choices[0].message.content)

# 将 AI 回复添加到对话历史,保持上下文连贯
messages.append({"role": "assistant", "content": response.choices[0].message.content})

# 第二轮对话
messages.append({"role": "user", "content": "你还记得我叫什么吗?"})
response = client.chat.completions.create(
    model="gpt-5",
    messages=messages
)
print(response.choices[0].message.content)
```

**示例 4:使用 Claude 模型**

```python
from openai import OpenAI

# 初始化 OpenAI 客户端
client = OpenAI(
    base_url="https://api.illm.io/v1",
    api_key="***"
)

# Claude 模型同样支持 OpenAI 格式调用
response = client.chat.completions.create(
    model="claude-sonnet-4-6",  # 使用 Claude Sonnet 4.6
    messages=[{"role": "user", "content": "解释一下量子计算的基本原理"}]
)

print(response.choices[0].message.content)
```

### 6.5.2 Node.js 示例

**示例 1:基本对话**

```javascript
import OpenAI from 'openai';

// 初始化 OpenAI 客户端,指向 iLLMHub 端点
const client = new OpenAI({
    baseURL: 'https://api.illm.io/v1',  // iLLMHub 主端点
    apiKey: '***'                        // 你的 API Key
});

// 创建对话请求
const response = await client.chat.completions.create({
    model: 'gpt-5',  // 使用 GPT-5 模型
    messages: [{ role: 'user', content: '你好,请介绍一下自己' }]
});

// 输出 AI 回复
console.log(response.choices[0].message.content);
```

**示例 2:流式输出**

```javascript
import OpenAI from 'openai';

// 初始化 OpenAI 客户端
const client = new OpenAI({
    baseURL: 'https://api.illm.io/v1',
    apiKey: '***'
});

// 创建流式请求,stream: true 启用流式输出
const stream = await client.chat.completions.create({
    model: 'gpt-5',
    messages: [{ role: 'user', content: '写一首关于春天的诗' }],
    stream: true
});

// 逐块接收并输出内容
for await (const chunk of stream) {
    process.stdout.write(chunk.choices[0]?.delta?.content || '');
}
```

### 6.5.3 curl 示例

**示例 1:基本对话(OpenAI 格式)**

```bash
# 使用 curl 调用 OpenAI 格式 API
curl https://api.illm.io/v1/chat/completions \
  -H "Authorization: Bearer ***" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-5",  # 模型名称
    "messages": [{"role": "user", "content": "你好"}]  # 消息内容
  }'
```

**示例 2:Claude 模型(Anthropic 格式)**

```bash
# 使用 curl 调用 Anthropic 格式 API
curl https://api.illm.io/v1/messages \
  -H "x-api-key: ***" \
  -H "content-type: application/json" \
  -H "anthropic-version: 2023-06-01" \
  -d '{
    "model": "claude-sonnet-4-6",  # Claude 模型名称
    "max_tokens": 1024,                    # 最大输出 Token 数
    "messages": [{"role": "user", "content": "你好"}]  # 消息内容
  }'
```

**示例 3:流式输出**

```bash
# 启用流式输出,stream 设为 true
curl https://api.illm.io/v1/chat/completions \
  -H "Authorization: Bearer ***" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-5",
    "messages": [{"role": "user", "content": "你好"}],
    "stream": true  # 启用流式输出
  }'
```

**示例 4:使用备用端点**

```bash
# 国内用户建议优先使用备用端点
curl https://api.illm.my/v1/chat/completions \
  -H "Authorization: Bearer ***" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-5",
    "messages": [{"role": "user", "content": "你好"}]  # 备用端点功能与主端点一致
  }'
```

---

## 6.6 常见问题 (FAQ)

### Q: 应该使用哪个 API 格式?

**A:** 推荐使用 **OpenAI 兼容格式**(`/v1/chat/completions`)。这个格式兼容性最好,几乎所有工具和库都支持,包括 Claude 模型也可以用这个格式调用。

### Q: 主端点和备用端点有什么区别?

**A:** 功能完全一样,只是网络线路不同。国内用户建议优先使用备用端点(`api.illm.my`),通常更稳定。

### Q: 如何判断请求是否成功?

**A:** 检查 HTTP 状态码:
- **200**:成功
- **4xx**:客户端错误(检查参数)
- **5xx**:服务器错误(稍后重试)

### Q: 流式输出和非流式输出有什么区别?

**A:**
- **非流式**:等待 AI 完整生成后一次性返回
- **流式**:AI 生成一部分就返回一部分,体验更流畅

### Q: temperature 参数应该设置多少?

**A:**
- **0.1-0.3**:稳定、确定性强的任务(代码生成、数据处理)
- **0.7-1.0**:创意性任务(写作、头脑风暴)
- **默认 1.0**:大多数场景适用

### Q: 如何实现多轮对话?

**A:** 在 `messages` 数组中包含历史消息:

```json
{
  "messages": [
    {"role": "user", "content": "我叫小明"},
    {"role": "assistant", "content": "你好,小明!"},
    {"role": "user", "content": "你还记得我叫什么吗?"}
  ]
}
```

---

## 本章小结

通过本章,你已经了解了:

- ✅ 主端点与备用端点的区别和选择方法
- ✅ OpenAI 兼容格式的请求参数和响应格式
- ✅ Anthropic 兼容格式的请求参数和响应格式
- ✅ 常见错误码和处理方法
- ✅ Python、Node.js、curl 的完整代码示例
- ✅ 多轮对话、流式输出等高级用法

**下一章预告**:第7章将详细介绍各种工具的配置方法,包括 Claude Code、Cursor、VS Code 等。

> 📷 **[截图占位:API 测试工具截图]** - 展示在控制台或工具中测试 API 调用的界面

---

## 7. 各工具配置教程

> **本章导读**:本章将详细介绍如何在各种开发工具中配置 iLLMHub,包括 Claude Code、Cursor、VS Code、OpenClaw 等主流工具,以及 Python、Node.js、curl 等编程语言的配置方法。读完本章后,你将能够熟练地在任何工具中使用 iLLMHub。

---

## 7.1 Claude Code 配置

### 7.1.1 什么是 Claude Code

Claude Code 是 Anthropic 官方的命令行 AI 编程助手,可以在终端中直接与 Claude 对话,帮助你编写、调试代码。

### 7.1.2 安装 Claude Code

```bash
# 使用 npm 安装
npm install -g @anthropic-ai/claude-code

# 验证安装
claude --version
```

### 7.1.3 配置环境变量

**方式一:临时设置(当前终端有效)**

```bash
export ANTHROPIC_BASE_URL=https://api.illm.io
export ANTHROPIC_API_KEY=***
```

**方式二:永久设置(推荐)**

```bash
# 添加到 ~/.zshrc 或 ~/.bashrc
echo 'export ANTHROPIC_BASE_URL=https://api.illm.io' >> ~/.zshrc
echo 'export ANTHROPIC_API_KEY=***' >> ~/.zshrc

# 使配置生效
source ~/.zshrc
```

> ⚠️ **注意**:
> - `ANTHROPIC_BASE_URL` 不要加 `/v1` 后缀,直接用 `https://api.illm.io` 即可。
> - **Claude Code v2 推荐使用 `~/.claude/settings.json` 配置文件**(优先级更高,避免环境变量被其他设置覆盖)。
> - 部分代理场景下可使用 `ANTHROPIC_AUTH_TOKEN` 取代 `ANTHROPIC_API_KEY`(v2.x 后备选项)。

### 7.1.4 验证配置

```bash
# 检查环境变量
echo $ANTHROPIC_BASE_URL
echo $ANTHROPIC_API_KEY

# 启动 Claude Code
claude
```

如果能正常进入对话界面,说明配置成功!

> 💡 **Claude Code v2 提示**:从 v2 起,环境变量在某些场景下不再覆盖 `~/.claude/settings.json` 中的 `ANTHROPIC_BASE_URL`。如果同时设置了环境变量与 settings.json,请检查优先级。如需确保生效,可使用配置文件。

### 7.1.5 常见问题

**问题 1:连接失败**
```text
Error: Connection refused
```

**解决方案**:
1. 检查 `ANTHROPIC_BASE_URL` 是否正确
2. 尝试切换到备用端点:`https://api.illm.my`
3. 检查网络连接

**问题 2:认证失败**
```text
Error: Invalid API key
```

**解决方案**:
1. 检查 `ANTHROPIC_API_KEY` 是否正确
2. 确认 Key 没有被禁用
3. 重新创建一个新的 Key

---

## 7.2 Cursor 配置

### 7.2.1 什么是 Cursor

Cursor 是一款 AI 编程 IDE,内置了 AI 对话和代码生成功能。

> ⚠️ **使用范围说明**:Cursor 近期版本中,自定义 OpenAI Base URL 主要对其 **Plan Mode(聊天/规划面板)** 生效。Composer、内联编辑、自动补全等仍使用 Cursor 自家后端,不会路由到 iLLMHub。如需在编程 Agent 中使用 iLLMHub 的全部模型,推荐使用 Claude Code、Codex CLI、Continue CLI 等完全支持自定义 Provider 的工具。
>
> 另:如果在 Cursor 中遇到"网络错误",请尝试在 `Cursor Settings > Network > HTTP Compatibility Mode` 中切换到 `HTTP/1.1`。

### 7.2.2 配置步骤

1. 打开 Cursor
2. 进入设置:`Cursor` → `Preferences` → `Settings`
3. 找到 `AI` 或 `Models` 部分
4. 配置以下参数:
   - **API Base URL**: `https://api.illm.io/v1`
   - **API Key**: `***`
5. 保存设置

### 7.2.3 验证配置

1. 打开 Cursor 的 AI 对话窗口
2. 输入一个问题
3. 如果能正常收到回复,说明配置成功

### 7.2.4 常见问题

**问题:模型不可用**

**解决方案**:
1. 确认模型名称正确(如 `gpt-5`、`claude-sonnet-4-6`)
2. 检查该模型是否在 iLLMHub 上可用
3. 尝试其他模型

---

## 7.3 VS Code + Continue 配置

### 7.3.1 什么是 Continue

Continue 是 VS Code 的开源 AI 编程助手插件(2026 年仍是 VS Code 主流 AI 插件之一),支持多种 AI 模型,完全支持自定义 OpenAI 兼容 Provider。

### 7.3.2 安装 Continue

1. 打开 VS Code
2. 进入扩展商店
3. 搜索 "Continue"
4. 点击安装

### 7.3.3 配置 Continue(2026 全新 YAML 格式)

> ⚠️ **配置格式变更**:Continue 已从 JSON 迁移到 **YAML** 配置文件。旧版 `config.json` 已被废弃,请改用 `config.yaml`。

1. 创建/打开 Continue 配置文件:`~/.continue/config.yaml`
2. 添加以下配置:

```yaml
name: My Config
version: 0.0.1
schema: v1
models:
  - name: GPT-5 (iLLMHub)
    provider: openai
    model: gpt-5
    apiBase: https://api.illm.io/v1
    apiKey: ***
  - name: Claude Sonnet 4.6 (iLLMHub)
    provider: openai
    model: claude-sonnet-4-6
    apiBase: https://api.illm.io/v1
    apiKey: ***
  - name: Claude Fable 5 (iLLMHub)
    provider: openai
    model: claude-fable-5
    apiBase: https://api.illm.io/v1
    apiKey: ***
  - name: DeepSeek V4 (iLLMHub)
    provider: openai
    model: deepseek-v4-pro
    apiBase: https://api.illm.io/v1
    apiKey: ***
```

3. 保存文件并重启 VS Code

### 7.3.4 验证配置

1. 打开 Continue 面板
2. 选择配置的模型
3. 输入问题测试

---

## 7.4 VS Code + Cline / Roo Code 配置

> **2026 推荐补充**:Cline 和 Roo Code 是 VS Code 中两个主流的 AI Agent 插件,**完整支持自定义 OpenAI 兼容 Provider**(不像 Cursor 那样仅 Plan Mode 生效)。如果需要完整编程 Agent 体验,这两个工具是 Cursor 的良好替代品。

### 7.4.1 什么是 Cline

Cline 是 VS Code 上的 AI Agent 插件,支持终端命令执行、文件编辑、浏览器自动化等完整 Agent 能力,完全支持自定义 OpenAI 兼容 API。

### 7.4.2 Cline 配置方法

1. 打开 VS Code,安装 Cline 插件
2. 点击 Cline 侧边栏图标,进入设置
3. 在 **API Provider** 下拉菜单中选择 **OpenAI Compatible**
4. 填写以下配置:
   - **Base URL**: `https://api.illm.io/v1`
   - **API Key**: `***`
   - **Model ID**: `gpt-5` / `claude-sonnet-4-6` / `claude-fable-5` 等
5. 保存即可使用

### 7.4.3 什么是 Roo Code

Roo Code 是 Cline 的一个活跃分支,2026-02-20 发布 v1 大版本,在 Cline 基础上优化了多模式(Mode)和工具调用体验。

### 7.4.4 Roo Code 配置方法

Roo Code 配置与 Cline 完全一致(都是 OpenAI 兼容接口),参考 7.4.2 即可。

> 💡 **小贴士**:Cline 和 Roo Code 都支持 Anthropic 原生格式和 OpenAI 兼容格式,推荐用 OpenAI 兼容格式(更通用)以调用 iLLMHub 上所有模型。

### 7.4.5 OpenAI Codex CLI(2026 编程 Agent)

Codex CLI 是 OpenAI 官方的终端编程 Agent,2025 年推出后持续演进,2026 年从 TypeScript 重写为 **Rust 版本**(0.139.0+),配置更简洁。

**安装与配置**:

```bash
# 安装 Codex CLI
npm install -g @openai/codex

# 设置环境变量指向 iLLMHub
export OPENAI_API_KEY=***
export OPENAI_BASE_URL=https://api.illm.io/v1

# 启动
codex
```

**使用自定义 Provider**(2026 推荐方式):

在 `~/.codex/config.toml` 中添加自定义 Provider 块,这里以 iLLMHub 为例:

```toml
model = "gpt-5"
model_provider = "illmhub"

[model_providers.illmhub]
name = "iLLMHub"
base_url = "https://api.illm.io/v1"
# wire_api 可选:"chat"(默认)或 "responses"(2026 新增)
wire_api = "chat"
```

> 💡 **小贴士**:
> - Codex CLI 也尊重 `OPENAI_BASE_URL` 环境变量,简单场景下可不用改 config.toml。
> - `wire_api = "responses"` 是 2026 新引入的选项,允许走 OpenAI Responses API。
> - 具体子命令请参考 `codex --help`。

## 7.5 OpenClaw 配置

### 7.5.1 什么是 OpenClaw

OpenClaw 是一个 AI Agent 框架,支持多种 AI 模型。

### 7.5.2 配置方法

在 `openclaw.json` 中添加 provider:

```json
{
  "models": {
    "providers": {
      "illmhub": {
        "baseUrl": "https://api.illm.io/v1",
        "api": "openai-completions",
        "apiKey": "***",
        "models": {
          "gpt-5": {},
          "claude-sonnet-4-6": {},
          "claude-fable-5": {},
          "gemini-3-pro": {},
          "deepseek-v3.2": {}
        }
      }
    }
  }
}
```

### 7.5.3 验证配置

```bash
# 检查配置
openclaw config get models.providers.illmhub

# 测试模型调用
openclaw chat --model illmhub/gpt-5 "你好"
```

---

## 7.6 Python 配置

### 7.6.1 使用 openai 库

**安装**:

```bash
# 安装 OpenAI Python 库
pip install openai
```

**基本使用**:

```python
from openai import OpenAI

# 初始化客户端,指向 iLLMHub
client = OpenAI(
    base_url="https://api.illm.io/v1",  # iLLMHub 端点
    api_key="***"                        # 你的 API Key
)

# 调用对话 API
response = client.chat.completions.create(
    model="gpt-5",  # 模型名称
    messages=[{"role": "user", "content": "你好"}]
)

# 输出回复
print(response.choices[0].message.content)
```

### 7.6.2 使用 anthropic 库

**安装**:

```bash
# 安装 Anthropic Python 库
pip install anthropic
```

**基本使用**:

```python
import anthropic

# 初始化 Anthropic 客户端
client = anthropic.Anthropic(
    base_url="https://api.illm.io",  # iLLMHub 端点(注意:不加 /v1)
    api_key="***"                     # 你的 API Key
)

# 调用 Claude 模型
response = client.messages.create(
    model="claude-sonnet-4-6",  # Claude 模型名称
    max_tokens=1024,                    # 最大输出 Token 数
    messages=[{"role": "user", "content": "你好"}]
)

# 输出回复
print(response.content[0].text)
```

### 7.6.3 环境变量配置

```python
import os
from openai import OpenAI

# 从环境变量读取配置,更安全
client = OpenAI(
    base_url=os.getenv("OPENAI_BASE_URL", "https://api.illm.io/v1"),  # 默认使用 iLLMHub
    api_key=os.getenv("OPENAI_API_KEY")                                # 从环境变量读取 Key
)
```

---

## 7.7 Node.js 配置

### 7.7.1 安装

```bash
# 安装 OpenAI Node.js 库
npm install openai
```

### 7.7.2 基本使用

```javascript
import OpenAI from 'openai';

// 初始化 OpenAI 客户端
const client = new OpenAI({
    baseURL: 'https://api.illm.io/v1',  // iLLMHub 端点
    apiKey: '***'                        // 你的 API Key
});

// 调用对话 API
const response = await client.chat.completions.create({
    model: 'gpt-5',  // 模型名称
    messages: [{ role: 'user', content: '你好' }]
});

// 输出回复
console.log(response.choices[0].message.content);
```

### 7.7.3 环境变量配置

```javascript
import OpenAI from 'openai';

// 从环境变量读取配置
const client = new OpenAI({
    baseURL: process.env.OPENAI_BASE_URL || 'https://api.illm.io/v1',  // 默认使用 iLLMHub
    apiKey: process.env.OPENAI_API_KEY                                  // 从环境变量读取 Key
});
```

---

## 7.8 curl 示例

### 7.8.1 OpenAI 格式

```bash
# 使用 curl 调用 OpenAI 格式 API
curl https://api.illm.io/v1/chat/completions \
  -H "Authorization: Bearer ***" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-5",  # 模型名称
    "messages": [{"role": "user", "content": "你好"}]  # 消息内容
  }'
```

### 7.8.2 Anthropic 格式

```bash
# 使用 curl 调用 Anthropic 格式 API
curl https://api.illm.io/v1/messages \
  -H "x-api-key: ***" \
  -H "content-type: application/json" \
  -H "anthropic-version: 2023-06-01" \
  -d '{
    "model": "claude-sonnet-4-6",  # Claude 模型名称
    "max_tokens": 1024,                    # 最大输出 Token 数
    "messages": [{"role": "user", "content": "你好"}]  # 消息内容
  }'
```

### 7.8.3 流式输出

```bash
# 启用流式输出
curl https://api.illm.io/v1/chat/completions \
  -H "Authorization: Bearer ***" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-5",
    "messages": [{"role": "user", "content": "你好"}],
    "stream": true  # 启用流式输出
  }'
```

---

## 7.9 常见问题 (FAQ)

### Q: 配置后无法连接怎么办?

**A:** 按以下顺序检查:
1. API Key 是否正确
2. 端点 URL 是否正确(注意是否有 `/v1`)
3. 网络连接是否正常
4. 尝试切换主/备端点

### Q: 如何查看支持的模型?

**A:** 登录 iLLMHub 后台,在"模型列表"页面查看。

---

## 本章小结

通过本章,你已经了解了:

- ✅ Claude Code 的安装和配置
- ✅ Cursor 的配置方法(及 Plan Mode 限制说明)
- ✅ VS Code + Continue 的配置(新 YAML 格式)
- ✅ VS Code + Cline / Roo Code 的配置(2026 补充)
- ✅ OpenAI Codex CLI 的配置
- ✅ OpenClaw 的配置
- ✅ Python、Node.js、curl 的代码示例
- ✅ 常见问题的解决方案

**下一章预告**:第8章将详细介绍 iLLMHub 支持的各种模型,帮助你选择最适合的模型。

> 📷 **[截图占位:Claude Code 环境变量配置界面截图]** - 展示在终端中设置环境变量的过程
> 📷 **[截图占位:Cursor 模型配置界面截图]** - 展示 Cursor 中添加自定义 OpenAI 兼容 provider 的配置面板
> 📷 **[截图占位:VS Code Continue 配置文件截图]** - 展示 config.yaml 中配置 iLLMHub 的示例
> 📷 **[截图占位:Cline / Roo Code 配置界面截图]** - 展示 Provider 设置面板
> 📷 **[截图占位:OpenClaw 配置截图]** - 展示 OpenClaw 的配置界面
> 📷 **[截图占位:Python 调用 iLLMHub 截图]** - 展示 Python 脚本成功调用 API 的输出

---

## 8. 支持的模型列表

> **本章导读**:本章将详细介绍 iLLMHub 支持的各种 AI 模型,包括 Claude、OpenAI、Gemini、DeepSeek 等系列,帮助你了解各模型的特点、适用场景,并提供模型选择指南。读完本章后,你将能够根据自己的需求选择最合适的模型。

---

## 8.1 Claude 系列(Anthropic)

Claude 是 Anthropic 公司开发的 AI 模型,以安全、有用、诚实著称。Anthropic 2025 下半年到 2026 上半年密集发布 Claude 4.5、4.6、4.7、4.8 系列,iLLMHub 同步跟进,可用的具体型号以平台后台为准。

### 8.1.1 Claude 模型概览

| 模型 | 特点 | 适用场景 |
|------|------|----------|
| `claude-fable-5` | **当前最强**(2026-05 发布),1M 上下文,128K 输出 | 最复杂任务、深度研究、高价值低频调用 |
| `claude-mythos-5` | Project Glasswing 参与者限定,顶级 | 项目限定场景 |
| `claude-sonnet-4-6` (及 4.5、4.7) | 高性能通用主力,推荐首选 | 代码生成、复杂推理、长文本处理、Agent 工作流 |
| `claude-opus-4-6` / `4-7` / `4-8` | 强推理能力,Opus 级智能 | 复杂分析、学术研究、深度 Agent 任务 |
| `claude-haiku-4-5` | 轻量快速,价格低 | 简单对话、快速响应、批量处理 |

> 💡 **提示**:手册中示例所用的具体模型 ID 会随版本更新而变化。实际调用时,请以平台后台"模型列表"为准。Anthropic 同时支持**别名**(如 `claude-sonnet-4-6`)和**快照 ID**(如 `claude-sonnet-4-5-20251015`),推荐使用别名。

### 8.1.2 Claude Sonnet 4.6(主力推荐)

**特点**:
- 性能接近 Opus 4 级别,但保持 Sonnet 价位
- 在 SWE-bench Verified、代码安全、规格遵守等基准上表现优秀
- 专为长时运行的 Agent 工作流优化,支持上下文跟踪与 Token 使用感知
- 支持 200K tokens 上下文

**适用场景**:
- 日常编程辅助、代码审查、调试
- 多步 Agent 任务、工具调用密集场景
- 文档编写、通用对话
- 生产环境主力模型(性价比最佳)

**示例**:
```python
response = client.chat.completions.create(
    model="claude-sonnet-4-6",
    messages=[{"role": "user", "content": "帮我写一个Python排序算法"}]
)
```

### 8.1.3 Claude Opus 系列(4.6 / 4.7 / 4.8)

**特点**:
- 最强推理能力,适合复杂任务
- Opus 4.7 于 2026-04-16 发布,Opus 4.8 于 2026-05 推出
- 价格较高,推荐用于需要高质量输出的关键场景
- 面向长上下文、多轮复杂思考

**适用场景**:
- 复杂代码架构设计、深度调试
- 学术研究、深度分析
- 创意写作、需要深度推理的任务
- 高价值低频率的关键调用

### 8.1.4 Claude Haiku 4.5

**特点**:
- 响应速度最快,价格最低
- 首个支持 extended thinking 和 context awareness 的 Haiku 模型
- 性能接近 Sonnet 4 级别,价格仅约 1/3
- 适合轻量、高频、大规模场景

**适用场景**:
- 快速问答、简单代码补全
- 批量处理、大规模部署
- 对响应速度和成本都敏感的场景

### 8.1.5 Claude Fable 5(2026-05 发布,当前最强)

**特点**:
- Anthropic 当前**广泛可用的最强模型**(比 Opus 4.8 更强)
- 1M tokens 上下文,128K max output
- **always-on adaptive thinking**(自适应思考机制持续开启)
- 适合最重要的复杂任务

**适用场景**:
- 最复杂的代码架构设计与调试
- 深度学术研究、系统性分析
- 高价值低频的关键调用
- 对输出质量要求最高、不计成本的任务

### 8.1.6 Claude Mythos 5(项目限定)

**特点**:
- Anthropic 顶级模型(与 Fable 5 同级)
- 仅限 **Project Glasswing 参与者**使用
- 1M tokens 上下文,128K max output

**适用场景**:
- 参与 Anthropic Glasswing 项目的特定场景
- 一般用户请使用 Claude Fable 5 获得近似顶级体验

---

## 8.2 OpenAI 系列

OpenAI 2025 年 8 月发布 GPT-5 之后,模型体系演进为 GPT-5 家族(gpt-5、gpt-5-mini、gpt-5-nano、gpt-5-pro),同时仍提供 GPT-4o 等上一代模型以保证兼容性。iLLMHub 跟进最新模型,具体可用型号以平台后台为准。

### 8.2.1 OpenAI 模型概览

| 模型 | 特点 | 适用场景 |
|------|------|----------|
| `gpt-5.5` | **当前最新旗舰**(2026-Q2),Frontier 级 | 最复杂任务、顶级输出质量 |
| `gpt-5` | 上代旗舰,400K 上下文 | 复杂任务、多模态理解、通用主力 |
| `gpt-5.3-codex` | 代码专用,Frontier 级 | 专业编程、代码生成、代码审查 |
| `gpt-5.1-codex-mini` | 轻量代码模型,价格低 | 日常代码补全、轻量编程 |
| `gpt-5-mini` | 平衡性能与成本,400K 上下文 | 日常对话、中等复杂度任务 |
| `gpt-5-nano` | 轻量快速,价格最低 | 快速问答、批量处理、高并发 |
| `gpt-5-pro` | 推理增强版旗舰,面向艰深任务 | 复杂推理、学术研究、高质量输出 |
| `o4-mini` | o 系列推理模型 | 数学、编程、科学问题 |
| `gpt-4.1` / `gpt-4o` / `gpt-4-turbo` | 上一代兼容模型 | 已有代码迁移过渡期使用 |

> 💡 **提示**:
> - OpenAI 同步提供 Chat Completions API 与 Responses API。iLLMHub 兼容 Chat Completions 路径(`/v1/chat/completions`),所有 GPT-5/5.5/Codex 家族模型均可用该路径调用。OpenAI 表示 Chat Completions API 将被 indefinitely 支持。
> - ⚠️ **重要变化**:**OpenAI Assistants API 将于 2026-08-26 关闭**。如果代码里还在用 Assistants API,请迁移到 **Responses API** + **Conversations API** 组合。Chat Completions 路径不受影响。

### 8.2.2 GPT-5(主力推荐)

**特点**:
- 400K tokens 上下文,128K max output
- 支持文本与图像输入(多模态)
- 在 coding、math、writing 等多维度上代际领先
- 可根据任务复杂度自适应计算

**适用场景**:
- 多模态任务(图文理解、视觉问答)
- 复杂通用对话、代码生成
- 内容创作、需要深度推理的任务

**示例**:
```python
response = client.chat.completions.create(
    model="gpt-5",
    messages=[{"role": "user", "content": "解释这张图片的内容"}]
)
```

### 8.2.3 GPT-5 mini / GPT-5 nano(成本优先)

**特点**:
- 同样 400K 上下文,但输出 token 限制 128K
- mini 适合中等复杂度任务,nano 适合高并发低延迟
- 价格阶梯明显,可根据预算选择

**适用场景**:
- GPT-5 mini:日常对话、客服、内容摘要
- GPT-5 nano:高并发请求、轻量分类、批量处理

### 8.2.4 GPT-5 pro(高质量推理)

**特点**:
- 面向最深推理需求,质量优先
- 价格较高,响应时间较长
- 适合低频高价值的艰深任务

**适用场景**:
- 数学问题求解
- 复杂算法设计
- 学术研究、科学计算
- 需要最高质量输出的任务

### 8.2.5 GPT-5.5(2026-Q2 最新旗舰)

**特点**:
- 当前 OpenAI 最强广泛可用模型
- 在 GPT-5 基础上进一步提升 coding、math、writing 多维能力
- 适合最重要、对质量要求最高的任务

**适用场景**:
- 最复杂的通用对话与多步推理
- 高质量多模态任务
- 代理、工具调用密集的关键任务

### 8.2.6 GPT-5.3-Codex(代码专用 Frontier)

**特点**:
- OpenAI 专门为编程场景优化的代码模型
- Frontier 级智能,价格与 GPT-5 接近
- 在代码生成、代码审查、调试场景下表现优秀

**适用场景**:
- 专业编程、复杂代码生成
- 代码审查、重构、调试
- 编程 Agent 场景

### 8.2.7 o4-mini(轻量推理模型)

**特点**:
- o 系列推理模型的轻量版本
- 在数学、编程、科学问题上表现优秀
- 价格低于完整 o 系列

**适用场景**:
- 中等复杂度的推理任务
- 需要思考能力但预算有限
- 与主对话模型配合使用做判断/评分

---

## 8.3 Gemini 系列(Google)

Google DeepMind 在 2025 年末到 2026 年上半年密集发布 Gemini 3、3.1、3.5 系列,Gemini 2.5 计划于 2026-10-16 退役。iLLMHub 同步跟进,推荐使用 Gemini 3.x 系列。

### 8.3.1 Gemini 模型概览

| 模型 | 特点 | 适用场景 |
|------|------|----------|
| `gemini-3-pro` | Google 旗舰,1M 上下文 | 复杂任务、多模态、超长文档分析 |
| `gemini-3.1-pro` | 3 Pro 升级版(2026-02-19) | 生产环境主力 |
| `gemini-3-pro-image` | 3 Pro 图像版(2025-11) | 图像生成与理解 |
| `gemini-3.5-flash` | 轻量快速,1M 上下文,性价比高 | 快速响应、批量处理 |
| `gemini-3.1-flash-image` | 3.1 Flash 图像版(2026-02) | 轻量图像生成 |
| `gemini-3.1-flash-lite` | 极轻量 Flash(2026-03) | 高并发低延迟 |
| `gemini-3.1-flash-audio` | 3.1 Flash 音频版(2026-04) | 实时语音/语音转文字 |
| `gemini-2.5-pro` / `gemini-2.5-flash` | 上一代主力,2026-10 退役 | 过渡期使用 |

> 💡 **提示**:Gemini 模型 ID 可能包含日期后缀(如 `gemini-3.1-pro-preview-2026xxxx`),实际可用型号以平台后台为准。

### 8.3.2 Gemini 3 Pro / 3.1 Pro

**特点**:
- Google 最新一代旗舰模型
- 1M tokens 超长上下文
- 多模态能力强(文本、图像、音频、视频)
- 在 GPQA Diamond、ARC-AGI-2 等推理基准上表现突出
- 3.1 Pro 在 2026-02-19 发布,2026-05 仍为 preview 阶段

**适用场景**:
- 超长文档分析(论文、代码库、报告)
- 多模态理解(图像问答、视频理解)
- 复杂推理、研究类任务
- Agent 场景、需要多步规划

### 8.3.3 Gemini 3.5 Flash(性价比首选)

**特点**:
- 1M tokens 上下文,但响应速度极快
- 价格低廉,性价比高
- 2026-05 在 Google I/O 2026 推出

**适用场景**:
- 快速问答、实时响应
- 批量处理、大规模部署
- 对成本敏感但需要长上下文的场景

---

## 8.4 DeepSeek 系列

DeepSeek 2025 年下半年到 2026 年上半年快速迭代,从 V3.1 到 V3.2 再到 V4 Preview。V4 在 2026-04-24 发布,首次以 1M tokens 上下文、1.6T 参数架构为亮点。iLLMHub 同步跟进国产高性价比模型。

### 8.4.1 DeepSeek 模型概览

| 模型 | 特点 | 适用场景 |
|------|------|----------|
| `deepseek-v4-pro` (Preview) | 1.6T 参数 MoE,49B 激活,1M 上下文 | 复杂推理、代码生成、中文任务 |
| `deepseek-v4-pro-max` (Preview) | V4 Pro 增强版,更高推理 effort | 最复杂推理、最高质量输出 |
| `deepseek-v4-flash` (Preview) | 284B 参数 MoE,13B 激活,1M 上下文 | 高并发低延迟、轻量生产环境 |
| `deepseek-v3.2` | V3 稳定主力,支持 Thinking in Tool-Use | 通用对话、Agent 场景 |
| `deepseek-v3.1` | V3.1 更新版 | 日常对话、内容创作 |

> 💡 **提示**:DeepSeek V4 系列在 Preview 阶段,具体可用性以平台后台为准。V4 Pro 的 1M 上下文下 FLOPs 仅为 V3.2 的 27%,KV cache 仅 10%,长上下文效率提升 10 倍。同期提供 Thinking 模式、Tool Calls、JSON Output、Context Caching 等高级能力。

### 8.4.2 DeepSeek V4 Pro(2026-04-24 Preview)

**特点**:
- 1.6T 总参数、49B 激活参数(MoE 架构)
- 1M tokens 超长上下文
- 引入三种推理模式(快速、平衡、深度思考)
- 世界知识更新到 2026 年
- 价格非常有竞争力
- 同步发布 `deepseek-v4-pro-max` 变体,提供更高推理 effort

**适用场景**:
- 复杂推理、数学、代码生成
- 中文场景(国产模型中文理解能力突出)
- 长上下文任务(论文分析、代码库理解)
- 对成本敏感的生产环境
- 需要最高质量输出时选 V4 Pro Max

### 8.4.3 DeepSeek V3.2(2025-12-01)

**特点**:
- 稳定主力,广泛适配各类应用
- 支持 Thinking in Tool-Use(推理中调用工具)
- 价格低,中文表现优秀
- 生态成熟、文档丰富

**适用场景**:
- 日常对话、中文内容创作
- Agent 与工作流场景
- 批量处理、成本敏感型部署

### 8.4.4 DeepSeek V4 Flash(轻量首选)

**特点**:
- 284B 参数 MoE,13B 激活参数
- 1M tokens 上下文
- 价格极低,适合大规模生产环境
- 长上下文效率比 V3.2 提升 10 倍(KV cache 减少)

**适用场景**:
- 高并发、低延迟服务
- 大规模批量处理
- 对成本极度敏感的生产部署
- 轻量 Agent 与工具调用场景

---

## 8.5 模型选择指南

### 8.5.1 按使用场景推荐

| 场景 | 推荐模型 | 理由 |
|------|---------|------|
| **顶级质量** | Claude Fable 5、GPT-5.5 | 当前最强,不计成本 |
| **日常对话** | GPT-5 mini、Claude Haiku 4.5 | 性价比高,响应快 |
| **代码生成** | Claude Sonnet 4.6、GPT-5.3-Codex | 代码能力强,代理友好 |
| **复杂推理** | Claude Opus 4.7/4.8、GPT-5 pro、o4-mini | 推理能力最强 |
| **长文档分析** | Gemini 3.1 Pro、DeepSeek V4-pro | 1M 上下文 |
| **多模态任务** | GPT-5、Gemini 3.1 Pro | 支持图文理解 |
| **实时音频/语音** | Gemini 3.1 Flash-audio | 专用语音模型 |
| **快速响应** | Claude Haiku 4.5、Gemini 3.5 Flash | 速度最快 |
| **低成本** | DeepSeek V4-flash、GPT-5 nano | 价格最低 |
| **中文任务** | DeepSeek V4 | 中文理解优秀,价格低 |
| **Agent / 工具调用** | Claude Sonnet 4.6、GPT-5、DeepSeek V3.2 | 支持复杂工具调用与长时运行 |

### 8.5.2 按预算推荐

**顶级预算(追求最高质量)**:
- Claude Fable 5
- GPT-5.5

**高预算(追求最佳效果)**:
- Claude Opus 4.8
- GPT-5 pro
- Claude Opus 4.7

**中等预算(平衡性能和成本)**:
- Claude Sonnet 4.6
- GPT-5
- Gemini 3.1 Pro
- DeepSeek V4-pro

**低预算(追求性价比)**:
- GPT-5 mini
- Claude Haiku 4.5
- Gemini 3.5 Flash
- DeepSeek V4-flash

### 8.5.3 模型选择决策树

```text
需要最高质量(不计成本)?
  → 是:Claude Fable 5 或 GPT-5.5
  → 否:继续

需要最强推理能力?
  → 是:Claude Opus 4.7/4.8、GPT-5 pro 或 o4-mini
  → 否:继续

需要处理超长文档(>200K)?
  → 是:Gemini 3.1 Pro 或 DeepSeek V4-pro(都支持 1M)
  → 否:继续

需要多模态(图像/视频)?
  → 是:GPT-5 或 Gemini 3.1 Pro
  → 否:继续

需要 Agent / 工具调用?
  → 是:Claude Sonnet 4.6 或 GPT-5
  → 否:继续

需要快速响应?
  → 是:Claude Haiku 4.5 或 Gemini 3.5 Flash
  → 否:继续

预算有限?
  → 是:DeepSeek V3.2 或 GPT-5 nano
  → 否:Claude Sonnet 4.6 或 GPT-5
```

---

## 8.6 Token 费率参考

### 8.6.1 费率说明

Token 费率因模型、供应商、活动而异,**强烈建议以 iLLMHub 后台实际显示为准**;若有出入,以 [第 10 章:技术支持](#10-技术支持) 为准。

下面给出参考价格区间(以官方公开价计,实际可能更优),仅供成本预估:

| 模型 | 输入价格(每 1M tokens) | 输出价格(每 1M tokens) | 说明 |
|------|---------|---------|------|
| Claude Opus 4.7 / 4.8 | $5 左右 | $25 左右 | 最强推理 |
| Claude Sonnet 4.6 | $3 左右 | $15 左右 | 主力推荐 |
| Claude Haiku 4.5 | $1 左右 | $5 左右 | 轻量快速 |
| GPT-5 | $1.25 | $10 | 最新旗舰 |
| GPT-5 mini | $0.25 | $2 | 平衡之选 |
| GPT-5 nano | $0.05 | $0.40 | 极低成本 |
| GPT-5 pro | $15 左右 | $120 左右 | 高质量推理 |
| Gemini 3 Pro | 中等 | 中等 | Google 旗舰(1M 上下文) |
| Gemini 3.5 Flash | 较低 | 较低 | 快速轻量(1M 上下文) |
| DeepSeek V4 | 很低 | $0.28 ~ $0.87 | 国产 1.6T MoE |
| DeepSeek V3.2 | 很低 | 很低 | 稳定主力 |

> 💡 **零基础提示**:
> - 上述价格为官方公开参考价。iLLMHub 作为聚合平台,实际费率可能更具竞争力,请以后台为准。
> - 还可以结合 prompt caching(高达 90% 节省)、batch API(50% 折扣)等能力进一步降低成本。

### 8.6.2 成本优化建议

1. **根据任务选择模型**:简单任务用轻量模型,复杂任务用旗舰模型
2. **控制输出长度**:设置合理的 `max_tokens` 值
3. **使用流式输出**:提升用户体验,不增加成本
4. **批量处理**:将多个任务合并,减少请求次数

---

## 8.7 常见问题 (FAQ)

### Q: 哪个模型最好?

**A:** 没有绝对的“最好”,要根据具体需求选择:
- 需要最高质量:Claude Fable 5 或 GPT-5.5
- 需要最强推理:Claude Opus 4.7/4.8 或 GPT-5 pro
- 需要 Agent / 长时运行:Claude Sonnet 4.6 或 GPT-5
- 需要快速响应:Claude Haiku 4.5 或 Gemini 3.5 Flash
- 需要性价比:DeepSeek V3.2 或 GPT-5 nano

### Q: 模型会更新吗?

**A:** 会的。AI 模型快速迭代,iLLMHub 会及时跟进。具体可用模型以平台后台实际显示为准;若有出入,以 [第 10 章:技术支持](#10-技术支持) 为准。

### Q: 如何知道模型是否可用?

**A:** 登录 iLLMHub 后台,在"模型列表"页面查看。部分模型可能因上游原因临时不可用。

### Q: 不同模型的上下文长度有什么区别?

**A:** 上下文长度决定了模型能处理的文本长度:
- Claude Sonnet/Opus:200K tokens
- GPT-5 家族:400K tokens(128K max output)
- Gemini 3 Pro / 3.1 Pro / 3.5 Flash:1M tokens
- DeepSeek V4 Pro / V4 Flash:1M tokens
- Claude Haiku 4.5:200K tokens

### Q: 为什么我用了手册里的模型 ID 报 404?

**A:** AI 模型迭代很快,手册中的具体模型 ID 可能会随版本变化。**请以平台后台“模型列表”里的实际可用型号为准**。如果手册中某个 ID 无法使用,通常是该型号已被升级或退役,可使用新版本(如 `claude-sonnet-4-6` 取代 `claude-sonnet-4-20250514`)。

### Q: OpenAI Assistants API 还能用吗?

**A:** ⚠️ OpenAI 宣布 **Assistants API 将于 2026-08-26 关闭**。如果你的代码仍在使用 Assistants API,请迁移到 **Responses API** + **Conversations API** 组合。Chat Completions API(`/v1/chat/completions`)不受影响,iLLMHub 仍然支持。

---

## 本章小结

通过本章,你已经了解了:

- ✅ Claude 系列(Sonnet 4.6/Opus 4.7-4.8/Haiku 4.5)模型的特点和适用场景
- ✅ OpenAI GPT-5 家族(gpt-5、gpt-5-mini、gpt-5-nano、gpt-5-pro)模型
- ✅ Gemini 3 / 3.1 / 3.5 系列的最新动态与 1M 上下文能力
- ✅ DeepSeek V3.2 / V4 Preview 的 1M 上下文与 1.6T MoE 架构
- ✅ 如何根据需求选择合适的模型
- ✅ Token 费率和成本优化建议

**下一章预告**:第9章将汇总常见问题解答,帮助你快速解决使用中的各种问题。
## 9. 常见问题 (FAQ)

### Q: API Key 无效 / 401 错误?

**A:** 请检查以下几点:
1. API Key 是否复制完整(不要遗漏字符)
2. Key 是否已过期或被禁用
3. 请求头格式是否正确(OpenAI 用 `Authorization: Bearer`,Anthropic 用 `x-api-key`)
4. 尝试重新创建一个新的 API Key

---

### Q: 请求超时怎么办?

**A:** 尝试以下方法:
1. **切换到备用端点**:将 API 地址从 `https://api.illm.io` 改为 `https://api.illm.my`
2. 检查本地网络连接
3. 如果使用代理,确认代理配置正确

---

### Q: 余额不足怎么办?

**A:** 登录后台(https://illmhub.ai),进入充值页面充值即可。充值后余额实时到账。

---

### Q: Claude Code 连接失败?

**A:** 请检查:
1. `ANTHROPIC_BASE_URL` 是否正确设置为 `https://api.illm.io`(注意:不要加 `/v1`)
2. `ANTHROPIC_API_KEY` 是否设置正确
3. 环境变量是否已生效(新开终端或执行 `source ~/.zshrc`)
4. 运行 `echo $ANTHROPIC_BASE_URL` 确认值正确

---

### Q: 如何查看用量和余额?

**A:** 登录 iLLMHub 后台(https://illmhub.ai),首页即可查看:
- 当前余额
- 历史用量统计
- API 调用记录

---

### Q: 支持流式输出吗?

**A:** 支持。在请求体中添加 `"stream": true` 即可启用流式输出,与官方 API 用法完全一致。

---

### Q: 国内网络访问慢?

**A:**
1. **使用备用端点** `https://api.illm.my`,通常国内访问更稳定
2. 如果仍然较慢,可以考虑配置网络代理

---

### Q: 支持哪些 API 格式?

**A:** iLLMHub 同时支持两种格式:
- **OpenAI 兼容格式**:`/v1/chat/completions`(适用于 GPT、Gemini、DeepSeek 等)
- **Anthropic 兼容格式**:`/v1/messages`(适用于 Claude 系列)

大多数工具和库默认使用 OpenAI 格式,直接配置 Base URL 为 `https://api.illm.io/v1` 即可。

---

### Q: 可以同时使用多个模型吗?

**A:** 可以。同一个 API Key 可以调用所有可用模型,只需在请求中指定 `model` 参数即可。

---

### Q: API Key 泄露了怎么办?

**A:** 立即进入后台的 API Key 管理页面,删除泄露的 Key 并重新创建一个新 Key。

---

### Q: 还能用 OpenAI Assistants API 吗?

**A:** ⚠️ OpenAI 宣布 **Assistants API 将于 2026-08-26 关闭**。如仍需相关能力,推荐迁移到 OpenAI 的 **Responses API** + **Conversations API**。iLLMHub 完整支持 Chat Completions 路径 `/v1/chat/completions`(以及 99% 的常见用法),不受本次退役影响。

---

## 10. 技术支持

如果遇到问题或有建议,可以通过以下方式联系我们:

- **官网**:https://illmhub.ai
- **联系邮箱**:support@illmhub.ai
- **用户群**:暂无 [待陛下提供]
- **文档站**:https://docs.illmhub.ai
- **状态页**:https://status.illmhub.ai [待陛下提供]

> ⚠️ **说明**:以上信息中标注 `[待陛下提供]` 的项为占位符,实际值需要陛下提供后更新。

---

## 11. 术语表

> **本章导读**:本章解释手册中出现的专业术语,帮助零基础用户理解 AI API 相关概念。

### 11.1 API 相关术语

| 术语 | 英文全称 | 解释 |
|------|----------|------|
| **API** | Application Programming Interface | 应用程序编程接口,是软件之间通信的桥梁。简单说,就是你和 AI 服务之间的"对话规则" |
| **API Key** | - | 你的专属访问密钥,用于身份验证和计费。类似密码,需妥善保管 |
| **端点** | Endpoint | API 的访问地址,如 `https://api.illm.io/v1`。不同端点可能对应不同服务器 |
| **RESTful API** | Representational State Transfer | 一种常见的 API 设计风格,使用 HTTP 方法(GET/POST)进行通信 |
| **HTTP 方法** | - | GET(获取数据)、POST(发送数据)、PUT(更新数据)、DELETE(删除数据) |
| **请求头** | Header | 发送 API 请求时附带的元数据,如认证信息、内容类型等 |
| **请求体** | Body | 发送 API 请求时携带的具体数据内容 |
| **响应** | Response | API 返回的结果数据 |
| **状态码** | Status Code | 200(成功)、401(认证失败)、429(频率限制)、500(服务器错误) |

### 11.2 模型相关术语

| 术语 | 解释 |
|------|------|
| **模型** | AI 模型,是经过训练的算法,能够理解自然语言并生成回复 |
| **大语言模型** | Large Language Model (LLM),专门处理文本的 AI 模型,如 GPT、Claude |
| **多模态** | Multimodal,支持多种输入类型(文本、图像、音频等)的模型 |
| **推理** | Inference,AI 模型处理输入并生成输出的过程 |
| **微调** | Fine-tuning,在预训练模型基础上,用特定数据进一步训练 |
| **上下文长度** | Context Length,模型能处理的最大文本长度,单位为 Token |
| **上下文窗口** | Context Window,模型一次能"看到"的全部内容范围 |

### 11.3 Token 相关术语

| 术语 | 解释 |
|------|------|
| **Token** | AI 处理文本的基本单位。英文中,1 个单词约 1-2 个 Token;中文中,1 个汉字约 1-2 个 Token |
| **输入 Token** | Prompt Tokens,发送给模型的文本长度 |
| **输出 Token** | Completion Tokens,模型生成的回复长度 |
| **Token 限制** | 模型单次请求能处理的最大 Token 数 |
| **计费** | 按 Token 用量收费,不同模型费率不同 |

### 11.4 对话相关术语

| 术语 | 解释 |
|------|------|
| **系统提示词** | System Prompt,设定 AI 行为的指令,如"你是一个编程助手" |
| **用户消息** | User Message,用户发送给 AI 的问题或指令 |
| **助手回复** | Assistant Message,AI 生成的回复内容 |
| **多轮对话** | Multi-turn Conversation,包含多组问答的连续对话 |
| **流式输出** | Streaming,AI 生成一部分就返回一部分,无需等待完整生成 |
| **温度** | Temperature,控制回复随机性的参数(0-2),值越高越随机 |
| **Top-p** | 核采样参数,控制候选 Token 的概率范围 |

### 11.5 平台相关术语

| 术语 | 解释 |
|------|------|
| **API 平台** | 聚合多家 AI 模型 API 并对外提供统一接入服务的平台 |
| **主端点** | Primary Endpoint,推荐使用的 API 地址 |
| **备用端点** | Backup Endpoint,主端点不可用时的替代地址 |
| **配额** | Quota,账户可用的资源限制(如请求次数、Token 数量) |
| **速率限制** | Rate Limit,单位时间内允许的最大请求数 |
| **延迟** | Latency,从发送请求到收到响应的时间 |

### 11.6 顶级模型与家族术语

| 术语 | 解释 |
|------|------|
| **顶级模型(Frontier Model)** | 同一代际中能力最强、面向高价值任务的模型,如 Claude Fable 5、GPT-5.5、Claude Opus 4.8 |
| **Claude Fable 5** | Anthropic 当前广泛可用的最强模型(2026-05 发布),1M 上下文,128K 输出 |
| **Claude Mythos 5** | Anthropic 顶级模型,Project Glasswing 项目限定 |
| **GPT-5.5** | OpenAI 当前最新旗舰(2026-Q2) |
| **GPT-5.3-Codex** | OpenAI 面向编程场景优化的代码专用模型 |
| **Gemini 3.1 Pro** | Google Gemini 主力旗舰(2026-02 发布),1M 上下文 |
| **DeepSeek V4 Pro** | 国产 1.6T MoE 顶级模型(2026-04-24 发布),1M 上下文 |
| **MoE 架构** | Mixture of Experts,多个专家子网络组合的大模型架构。V4 Pro 总参数 1.6T,激活 49B |
| **1M 上下文** | 模型能一次处理的文本长度为 100 万 tokens,约相当于 75 万中文字或 50 万英文单词 |
| **快照 ID** | Snapshot ID,如 `claude-sonnet-4-5-20251015`,锁定到特定发布日期的模型版本 |
| **别名** | Alias,如 `claude-sonnet-4-6`,Anthropic 推荐用法,自动指向最新快照 |
| **Thinking 模式** | DeepSeek 特有,模型在工具调用中仍保持推理能力 |
| **Responses API** | OpenAI 新一代 API 原语,2025-03 推出,集成 web search、file search、computer use 等能力 |

---

## 12. 快速参考卡

> **本章导读**:一页纸速查表,包含常用端点、模型、命令等关键信息,建议收藏备用。

### 12.1 端点速查

| 用途 | 地址 | 备注 |
|------|------|------|
| 主端点 | `https://api.illm.io` | 推荐,海外优先 |
| 备用端点 | `https://api.illm.my` | 国内优先 |
| OpenAI 格式路径 | `/v1/chat/completions` | 适用所有模型 |
| Anthropic 格式路径 | `/v1/messages` | 仅适用 Claude |

### 12.2 模型速查

| 场景 | 推荐模型 | 说明 |
|------|----------|------|
| 顶级质量 | Claude Fable 5、GPT-5.5 | 当前最强(2 个顶级选项) |
| 日常对话 | GPT-5-mini、Claude Haiku 4.5 | 性价比高 |
| 代码生成 | Claude Sonnet 4.6、GPT-5.3-Codex | 代码能力强 |
| 复杂推理 | Claude Opus 4.8、GPT-5 pro、o4-mini | 推理能力最强 |
| 超长文档 | Gemini 3.1 Pro、DeepSeek V4-pro | 1M 上下文 |
| 低成本 | DeepSeek V4-flash、GPT-5 nano | 价格最低 |

### 12.3 关键参数速查

| 参数 | 值 | 说明 |
|------|-----|------|
| `model` | `gpt-5` / `claude-sonnet-4-6` | 模型名称 |
| `stream` | `true` / `false` | 是否流式输出 |
| `temperature` | 0-2(默认 1.0) | 值越高越随机 |
| `max_tokens` | 整数 | 最大输出 Token |
| `messages` | 数组 | 对话历史 |

### 12.4 常用代码片段

**Python 基本调用**:
```python
from openai import OpenAI
client = OpenAI(base_url="https://api.illm.io/v1", api_key="***")
response = client.chat.completions.create(model="gpt-5", messages=[{"role": "user", "content": "你好"}])
print(response.choices[0].message.content)
```

**curl 基本调用**:
```bash
curl https://api.illm.io/v1/chat/completions \
  -H "Authorization: Bearer ***" \
  -H "Content-Type: application/json" \
  -d '{"model": "gpt-5", "messages": [{"role": "user", "content": "你好"}]}'
```

### 12.5 环境变量速查

| 工具 | 变量 | 值 |
|------|------|-----|
| Claude Code | `ANTHROPIC_BASE_URL` | `https://api.illm.io` |
| Claude Code | `ANTHROPIC_API_KEY` | 你的 Key |
| 通用 OpenAI (macOS/Linux) | `OPENAI_BASE_URL` | `https://api.illm.io/v1` |
| 通用 OpenAI (macOS/Linux) | `OPENAI_API_KEY` | 你的 Key |
| 通用 OpenAI (Windows CMD) | `OPENAI_BASE_URL` | `set OPENAI_BASE_URL=https://api.illm.io/v1` |
| 通用 OpenAI (Windows CMD) | `OPENAI_API_KEY` | `set OPENAI_API_KEY=你的 Key` |
| 通用 OpenAI (Windows PowerShell) | `OPENAI_BASE_URL` | `$env:OPENAI_BASE_URL="https://api.illm.io/v1"` |
| 通用 OpenAI (Windows PowerShell) | `OPENAI_API_KEY` | `$env:OPENAI_API_KEY="你的 Key"` |

### 12.6 常见错误速查

| 错误码 | 含义 | 解决方案 |
|--------|------|----------|
| 400 | 请求格式错误 | 检查请求体 JSON 格式与必填参数 |
| 401 | 认证失败 | 检查 API Key |
| 403 | 无权限 | 检查 Key 是否被禁用或模型是否可用 |
| 404 | 端点/模型不存在 | 检查 URL 路径与模型 ID(手册中的 ID 可能已升级) |
| 429 | 频率限制 | 降低请求频率或联系客服提升限额 |
| 500 | 服务器错误 | 稍后重试 |
| 502 | 网关错误 | 切换端点 |
| 503 | 服务不可用 | 稍后重试或切换端点 |

---

## 13. 最佳实践

> **本章导读**:本章总结了使用 iLLMHub 的最佳实践,帮助你安全、高效、经济地使用 AI API。

---

### 13.1 API Key 安全最佳实践

#### 13.1.1 基本原则

1. **不要硬编码**:永远不要将 API Key 直接写在代码中
2. **不要提交**:确保 API Key 不被提交到 Git 仓库
3. **不要分享**:不要将 API Key 分享给他人
4. **定期轮换**:定期更换 API Key

#### 13.1.2 安全存储方法

**方法一:环境变量(推荐)**
```bash
# Linux/macOS
export OPENAI_API_KEY=sk-xxxx

# Windows(PowerShell)
$env:OPENAI_API_KEY="sk-xxxx"
```

**方法二:.env 文件**
```bash
# .env 文件
OPENAI_API_KEY=sk-xxxx

# .gitignore 文件
.env
```

**方法三:密钥管理服务**
- AWS Secrets Manager
- HashiCorp Vault
- 1Password CLI

#### 13.1.3 泄露应急处理

如果 API Key 泄露:
1. **立即删除**:登录后台删除泄露的 Key
2. **重新创建**:创建新的 API Key
3. **检查用量**:查看是否有异常调用
4. **更新配置**:更新所有使用该 Key 的应用

---

### 13.2 成本优化最佳实践

#### 13.2.1 模型选择策略

| 任务类型 | 推荐模型 | 理由 |
|----------|----------|------|
| 简单对话 | GPT-4o-mini | 成本低,速度快 |
| 代码生成 | Claude Sonnet | 性价比高 |
| 复杂推理 | Claude Opus | 质量最好 |
| 批量处理 | DeepSeek Chat | 价格最低 |

#### 13.2.2 Token 节省技巧

1. **精简提示词**:避免冗长的系统提示
2. **控制输出长度**:设置合理的 `max_tokens`
3. **使用流式输出**:提升用户体验,不增加成本
4. **批量处理**:将多个任务合并,减少请求次数

#### 13.2.3 成本监控

```python
# 在响应中查看 Token 用量
response = client.chat.completions.create(...)
usage = response.usage
print(f"输入 Token: {usage.prompt_tokens}")
print(f"输出 Token: {usage.completion_tokens}")
print(f"总计 Token: {usage.total_tokens}")
```

---

### 13.3 性能优化最佳实践

#### 13.3.1 网络优化

1. **选择合适的端点**:
   - 国内用户:优先使用 `api.illm.my`
   - 海外用户:优先使用 `api.illm.io`

2. **使用连接池**:
```python
import httpx

client = httpx.Client(
    base_url="https://api.illm.io/v1",
    headers={"Authorization": "Bearer sk-xxxx"},
    timeout=30.0
)
```

3. **启用压缩**:
```python
client = OpenAI(
    base_url="https://api.illm.io/v1",
    api_key="sk-xxxx",
    http_client=httpx.Client(compression=True)
)
```

#### 13.3.2 并发处理

```python
import asyncio
from openai import AsyncOpenAI

async def call_api(prompt: str):
    client = AsyncOpenAI(
        base_url="https://api.illm.io/v1",
        api_key="sk-xxxx"
    )
    response = await client.chat.completions.create(
        model="gpt-5",
        messages=[{"role": "user", "content": prompt}]
    )
    return response.choices[0].message.content

# 并发调用多个请求
async def main():
    tasks = [call_api(f"问题 {i}") for i in range(5)]
    results = await asyncio.gather(*tasks)
    return results
```

---

### 13.4 错误处理最佳实践

#### 13.4.1 重试机制

```python
import time
from openai import OpenAI, APIError, RateLimitError

def call_with_retry(client, model, messages, max_retries=3):
    for attempt in range(max_retries):
        try:
            response = client.chat.completions.create(
                model=model,
                messages=messages
            )
            return response
        except RateLimitError:
            if attempt < max_retries - 1:
                wait_time = 2 ** attempt  # 指数退避
                print(f"频率限制,等待 {wait_time} 秒后重试...")
                time.sleep(wait_time)
            else:
                raise
        except APIError as e:
            if attempt < max_retries - 1:
                print(f"API 错误: {e},重试中...")
                time.sleep(1)
            else:
                raise
```

#### 13.4.2 异常处理

```python
try:
    response = client.chat.completions.create(...)
except Exception as e:
    print(f"错误类型: {type(e).__name__}")
    print(f"错误信息: {e}")
    # 根据错误类型采取不同措施
    if "401" in str(e):
        print("API Key 无效,请检查")
    elif "429" in str(e):
        print("请求过于频繁,请稍后重试")
    elif "500" in str(e):
        print("服务器错误,请稍后重试")
```

---

### 13.5 生产环境部署建议

#### 13.5.1 环境变量管理

```bash
# .env.production
OPENAI_API_KEY=sk-xxxx
OPENAI_BASE_URL=https://api.illm.io/v1

# 应用配置
API_TIMEOUT=30
MAX_RETRIES=3
```

#### 13.5.2 监控与告警

1. **监控指标**:
   - API 调用次数
   - 响应时间
   - 错误率
   - Token 用量

2. **告警规则**:
   - 错误率 > 5%
   - 响应时间 > 5秒
   - 余额 < 10元

#### 13.5.3 备份方案

1. **主备端点切换**:配置自动切换逻辑
2. **多模型降级**:主模型不可用时自动切换备用模型
3. **本地缓存**:缓存常用请求结果

---

### 13.6 团队协作最佳实践

#### 13.6.1 API Key 管理

1. **按环境分离**:开发、测试、生产使用不同 Key
2. **按项目分离**:不同项目使用不同 Key
3. **权限控制**:根据团队成员角色分配不同权限的 Key

#### 13.6.2 成本分摊

在生产环境中,建议按项目或按团队维度拆分 API Key,便于后续按用量做成本分摊与对账。具体可在后台为不同项目创建独立的 API Key,再在每个项目的配置中分别使用对应的 Key。

---

## 14. 故障排查流程图

> **本章导读**:本章提供常见问题的排查流程图,帮助你快速定位和解决问题。

---

### 14.1 连接失败排查流程

```text
连接失败
    │
    ├─→ 检查网络连接
    │   ├─→ 无法访问互联网
    │   │   └─→ 检查网络设置、重启路由器
    │   └─→ 可以访问互联网
    │       ├─→ 检查端点地址
    │       │   ├─→ 地址错误
    │       │   │   └─→ 修正为正确地址
    │       │   └─→ 地址正确
    │       │       ├─→ 尝试备用端点
    │       │       │   ├─→ 备用端点可用
    │       │       │   │   └─→ 使用备用端点
    │       │       │   └─→ 备用端点也不可用
    │       │       │       └─→ 服务器问题,稍后重试
    │       │       └─→ 检查防火墙设置
    │       └─→ 联系技术支持
    └─→ 结束
```

**快速检查清单:**
- [ ] 网络连接正常
- [ ] 端点地址正确
- [ ] 尝试备用端点
- [ ] 防火墙未阻止

---

### 14.2 认证失败排查流程

```text
认证失败(401)
    │
    ├─→ 检查 API Key
    │   ├─→ Key 为空
    │   │   └─→ 设置 API Key
    │   └─→ Key 已设置
    │       ├─→ Key 格式错误
    │       │   └─→ 检查 Key 格式(sk-xxxx)
    │       └─→ Key 格式正确
    │           ├─→ Key 已过期/禁用
    │           │   └─→ 登录后台检查 Key 状态
    │           └─→ Key 有效
    │               ├─→ 请求头格式错误
    │               │   ├─→ OpenAI 格式: Authorization: Bearer sk-xxxx
    │               │   └─→ Anthropic 格式: x-api-key: sk-xxxx
    │               └─→ 联系技术支持
    └─→ 结束
```

**快速检查清单:**
- [ ] API Key 已设置
- [ ] Key 格式正确(sk-xxxx)
- [ ] Key 未过期/禁用
- [ ] 请求头格式正确

---

### 14.3 响应慢排查流程

```text
响应慢
    │
    ├─→ 检查网络延迟
    │   ├─→ 延迟高(>200ms)
    │   │   ├─→ 国内用户
    │   │   │   └─→ 切换到备用端点(api.illm.my)
    │   │   └─→ 海外用户
    │   │       └─→ 切换到主端点(api.illm.io)
    │   └─→ 延迟正常
    │       ├─→ 检查模型选择
    │       │   ├─→ 使用大型模型(Opus/GPT-4o)
    │       │   │   └─→ 大型模型本身较慢,考虑降级
    │       │   └─→ 使用小型模型
    │       │       ├─→ 检查 Token 数量
    │       │       │   ├─→ 输入 Token 过多
    │       │       │   │   └─→ 精简输入内容
    │       │       │   └─→ 输出 Token 过多
    │       │       │       └─→ 设置 max_tokens
    │       │       └─→ 检查服务器状态
    │       │           ├─→ 服务器负载高
    │       │           │   └─→ 稍后重试
    │       │           └─→ 服务器正常
    │       │               └─→ 联系技术支持
    └─→ 结束
```

**快速检查清单:**
- [ ] 网络延迟正常
- [ ] 选择合适的模型
- [ ] 控制 Token 数量
- [ ] 设置合理的超时时间

---

### 14.4 常见错误代码解决

#### 14.4.1 400 Bad Request

**原因**:请求格式错误

**排查步骤:**
1. 检查请求体 JSON 格式
2. 检查必填参数是否完整
3. 检查参数类型是否正确

**示例修复:**
```python
# 错误:messages 格式错误
response = client.chat.completions.create(
    model="gpt-5",
    messages="你好"  # ❌ 应该是数组
)

# 正确:
response = client.chat.completions.create(
    model="gpt-5",
    messages=[{"role": "user", "content": "你好"}]  # ✅
)
```

---

#### 14.4.2 429 Too Many Requests

**原因**:请求频率超过限制

**解决方案:**
1. **降低请求频率**:添加延迟
2. **实现重试机制**:使用指数退避
3. **申请更高配额**:联系技术支持

```python
import time

for i in range(10):
    try:
        response = client.chat.completions.create(...)
        break
    except RateLimitError:
        time.sleep(2 ** i)  # 指数退避
```

---

#### 14.4.3 500 Internal Server Error

**原因**:服务器内部错误

**解决方案:**
1. **稍后重试**:通常是临时问题
2. **切换端点**:尝试备用端点
3. **检查状态页**:查看是否有服务中断公告

---

#### 14.4.4 502 Bad Gateway

**原因**:网关错误

**解决方案:**
1. **切换端点**:立即切换到备用端点
2. **等待恢复**:通常是临时问题
3. **联系技术支持**:如果持续出现

---

### 14.5 高级排查技巧

#### 14.5.1 启用详细日志

```python
import logging

logging.basicConfig(level=logging.DEBUG)
logging.getLogger("httpx").setLevel(logging.DEBUG)
```

#### 14.5.2 抓包分析

```bash
# 使用 curl 测试
curl -v https://api.illm.io/v1/chat/completions \
  -H "Authorization: Bearer sk-xxxx" \
  -H "Content-Type: application/json" \
  -d '{"model": "gpt-5", "messages": [{"role": "user", "content": "test"}]}'
```

#### 14.5.3 检查服务器状态

- 访问 iLLMHub 官网查看公告
- 检查常见问题及 FAQ 中是否有类似问题
- 联系技术支持获取帮助

---
