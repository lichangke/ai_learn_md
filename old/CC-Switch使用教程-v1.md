[toc]

# CC-Switch 使用教程（Windows）：配置并“中转/转发”到 Codex

这篇文章用通俗的方式，带你在 **Windows** 上完成：

- 下载并安装 **CC-Switch**
- 检查必要环境（如 Node.js）
- 在 CC-Switch 里添加 **Codex** 的配置（填写 API Key 与请求地址）

如果你只是想快速跑起来，可以直接跳到「Codex 配置」一节照着做。

---

# 1. CC-Switch 是什么？能做什么？

**CC-Switch** 可以把多个 AI 工具/模型相关的配置集中管理，并在不同供应商（Provider）之间切换。常见使用场景包括：

- 同时管理 Claude Code、Codex、Gemini、OpenCode 等工具的账号/接口配置
- 管理 MCP 服务器（用于把外部能力接入到 AI 工具里）
- 管理 Skills（可理解为“插件/扩展”）
- 管理系统提示词（System Prompt）

本文重点：在 Windows 上用 CC-Switch 配置 **Codex**，并把请求“转发/中转”到你所使用的服务商接口。

---

# 2. 准备工作（开始前先确认）

建议你先确认下面几项，避免做到一半卡住：

1. **你已安装 Codex（或准备使用 Codex）**
2. 你有可用的 **API Key**
3. 你知道对应服务商的 **API 请求地址（Base URL / Endpoint）**
4. （可选但推荐）本机已安装 **Node.js**

> 提醒：API Key 属于敏感信息，不要截图公开，不要上传到公开仓库或群聊。

---

# 3. CC-Switch 下载与安装（Windows）

1. 打开 CC-Switch 中文说明（包含功能说明、系统要求与下载入口）：
   - README_ZH.md：<https://github.com/farion1231/cc-switch/blob/main/README_ZH.md>
2. 打开 Releases 页面下载安装包：
   - Releases：<https://github.com/farion1231/cc-switch/releases>
3. 在 Releases 页面往下滚动，找到与你的系统与架构匹配的安装包（例如 Windows x64），然后下载并安装。
   - 参考截图：
     ![1770459123431](images/CC-Switch使用教程/1770459123431.png)
4. 安装完成后运行 CC-Switch，界面示例：
   ![1770459207489](images/CC-Switch使用教程/1770459207489.png)

---

# 4. 检查 Node.js 环境（推荐）

有些功能可能依赖 Node.js。你可以用下面方式快速确认是否已安装：

在 **cmd** 或 **PowerShell** 中运行：

```bash
node --version
```

- 如果已安装，会输出版本号（例如 `v20.x.x`）：
  ![1770459511992](images/CC-Switch使用教程/1770459511992.png)
- 如果提示“找不到命令/不是内部或外部命令”，说明未安装 Node.js，需要先安装：
  - 参考教程：<https://www.runoob.com/nodejs/nodejs-install-setup.html>
  - 参考截图：
    ![1770459636302](images/CC-Switch使用教程/1770459636302.png)

---

# 5. Codex 配置（在 CC-Switch 中添加/切换）

在开始配置前，请先准备好两样东西：

- **API Key**
- **API 请求地址（Base URL / Endpoint）**

操作步骤：

1. 在 CC-Switch 中找到 **Codex** 入口，点击进入后，再点击「+」新增配置：
   ![1770459760575](images/CC-Switch使用教程/1770459760575.png)
2. 选择供应商/模型：
   - 如果列表里有你要用的 **预设供应商**，直接选即可
   - 如果没有，就选择 **自定义**（按你的服务商要求填写）
   ![1770459825893](images/CC-Switch使用教程/1770459825893.png)
3. 填写 **API Key** 与 **API 请求地址**，保存即可：
   ![1770467845871](images/CC-Switch使用教程/1770467845871.png)

补充说明（很重要）：

- 不同服务商的 **API Key** 与 **请求地址** 都不一样，请以服务商的官方文档为准。
- 如果你使用的是“中转/代理”类服务，请确认它提供的是 **兼容的 Endpoint**（例如 OpenAI 兼容或其他协议），并按它要求填写 Base URL。
- 遇到调用失败时，优先检查三件事：Key 是否有效、Base URL 是否写对、网络/代理是否能访问服务商。

---

# 6. 常见问题（排查思路）

- **CC-Switch 能打开但请求失败**
  - 多半是 API Key/Base URL 有误，或网络不可达；先对照服务商文档核对。
- **提示未安装 Node.js**
  - 按第 4 节安装 Node.js，再重新打开 CC-Switch。
- **我不知道 Base URL 应该填什么**
  - 只能去你所使用服务商的文档里查“API Endpoint/Base URL”；不同平台不通用。

---

# 术语解释

- **Provider（供应商）**：提供模型接口的服务方（官方/中转/代理都算）。
- **Model（模型）**：你实际调用的 AI 模型名称或版本。
- **MCP（Model Context Protocol）**：一种把外部工具/数据接入到 AI 工具里的协议/机制（不同工具支持程度不同）。
- **Skills**：可理解为插件/扩展，让工具拥有额外能力（例如调用外部服务、执行特定工作流）。
- **System Prompt（系统提示词）**：给 AI 的“全局规则/角色设定”，影响它的回答风格与边界。
- **API Key**：调用接口的密钥（相当于账号密码的一种）。
- **Endpoint / Base URL（请求地址）**：接口请求的基础地址（不同服务商不同，填错会直接连不上）。

