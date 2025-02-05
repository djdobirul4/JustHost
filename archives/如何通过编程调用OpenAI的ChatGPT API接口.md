# 如何通过编程调用OpenAI的ChatGPT API接口

## 前言

最近大火的ChatGPT提供了一系列API接口，可以调用多种模型进行对话，实现以下功能：

- 起草电子邮件或其他书面文件
- 编写代码
- 回答有关一组文件的问题
- 创建会话代理
- 为您的软件提供自然语言界面
- 一系列科目的导师
- 翻译语言
- 模拟视频游戏中的角色等等

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bbtdd.com/WildCard)

## 准备工作

在开始之前，您需要完成以下准备工作：

1. **注册OpenAI账号**：您需要先注册一个OpenAI账号，并获取API访问权限。
2. **Python开发环境**：确保您的Python版本在3.7.1及以上。

## 获取开发Key

1. 访问 [OpenAI API Keys](https://platform.openai.com/account/api-keys)。
2. 点击“Create new secret key”按钮。
3. 输入任意Key名称，并生成Key。
4. 复制并保存您的Secret Key，因为一旦关闭对话框，Key将无法再次查看。

## 开发步骤

### 安装OpenAI库

首先，通过pip安装OpenAI库：

bash
pip install openai


### 编写示例代码

创建一个新的脚本文件 `helloai.py`，并编写以下代码：

python
import os
import openai

# 填入你的OPENAI_API_KEY
openai.api_key = "OPENAI_API_KEY"

# 这里我们使用的模型是gpt-3.5-turbo
# 使用角色为user，提问的内容是：Hello!
completion = openai.ChatCompletion.create(
  model="gpt-3.5-turbo",
  messages=[
    {"role": "user", "content": "Hello!"}
  ]
)

# 输出生成的内容
print(completion.choices[0].message)

# 把整个响应输出一下
print(completion)


### 运行脚本

通过以下命令运行脚本：

bash
python ./helloai.py


### 输出结果

您将看到类似以下输出：

bash
Hello there, how may I assist you today?
{
  "id": "chatcmpl-123",
  "object": "chat.completion",
  "created": 1677652288,
  "choices": [{
    "index": 0,
    "message": {
      "role": "assistant",
      "content": "\n\nHello there, how may I assist you today?",
    },
    "finish_reason": "stop"
  }],
  "usage": {
    "prompt_tokens": 9,
    "completion_tokens": 12,
    "total_tokens": 21
  }
}


## 代理设置

由于OpenAI服务器在某些地区无法直接访问，您可能需要设置代理。可以通过以下方式解决：

1. **全局科学上网**：确保您的网络环境可以访问OpenAI服务器。
2. **设置代理**：在代码中添加代理设置。

python
openai.proxy = "http://127.0.0.1:1080"


## 模型参数

`model`参数用于指定API使用的对话生成模型，目前支持的模型包括：

- gpt-4、gpt-4-0314、gpt-4-32k、gpt-4-32k-0314
- gpt-3.5-turbo、gpt-3.5-turbo-0301

## 消息参数

`messages`参数是当前对话的列表，包含以下角色：

- **system**：系统角色，提供初始指令或规则。
- **user**：用户提问的文本内容。
- **assistant**：ChatGPT返回的内容，用于多轮对话。

## Token概念

OpenAI根据对话和生成词量（Token）来计费。您可以通过`max_tokens`参数控制生成的最大Token数量，以避免过度消耗。

## 完整示例

以下是一个命令行交互式输入的示例，启动后输入问题，然后回车。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bbtdd.com/WildCard)