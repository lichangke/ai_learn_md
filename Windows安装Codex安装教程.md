[toc]

# Windows 安装 Codex CLI 教程

这篇文章面向**纯新手小白**：你不需要懂太多命令行，也不需要把 Codex 装到 WSL 里（本文**只讲原生 Windows 安装**）。

你将完成：

- 在 Windows 10/11 上装好 Node.js（含 npm）
- 通过 npm 安装 Codex CLI
- 完成首次运行（登录或配置 API Key）
- 学会升级/卸载

---

## 0. 一句话流程（先看这个，心里有底）

![安装流程总览](images/Windows安装Codex安装教程/01-安装流程总览.png)

如果你只想按最短路径走，记住这 4 句：

1. 用 `winget` 装 Node.js LTS
2. 用 `npm` 全局安装 `@openai/codex`
3. 用 `codex --version` 验证
4. 运行 `codex`，按提示登录/配置

---

# 1. 开始前准备（3 分钟检查清单）

## 1.1 你需要满足什么条件？

- **系统**：Windows 10/11（建议已更新到较新版本）
- **终端**：PowerShell（系统自带即可；更推荐 Windows Terminal）
- **网络**：能访问 OpenAI 相关服务（公司网络/校园网可能需要代理）
- **权限**：能安装软件（建议用自己的电脑；公司电脑可能被策略限制）

## 1.2 建议你先装好（可选但强烈建议）

- Windows Terminal（更好用的终端）
- Git（后面用 Codex 改代码/提交会方便很多）

如果你电脑支持 `winget`，这两条命令可以直接装（可选）：

```powershell
winget install Microsoft.WindowsTerminal
winget install Git.Git
```

> 下图是“你要打开什么终端、在什么地方敲命令”的直观示意。
>
> ![终端与命令在哪敲](images/Windows安装Codex安装教程/02-终端与命令位置.png)

---

# 2. 检查你的电脑：Node/npm/Git 是否已存在

先打开 **PowerShell**（开始菜单搜索“PowerShell”即可，不一定要管理员）。

复制粘贴执行下面这些命令（可以一条条执行）：

```powershell
node -v
npm -v
git --version
```

你会遇到两种情况：

- ✅ 能看到版本号：说明已装好，直接跳到第 4 章装 Codex
- ❌ 提示“找不到命令 / 不是内部或外部命令”：说明没装或 PATH 没配好，继续看第 3 章

---

# 3. 安装 Node.js（含 npm）——推荐用 winget

Codex CLI 是通过 **npm** 安装的，而 npm 跟着 Node.js 一起装，所以你先把 Node.js 安好就行。

## 3.1 方法 A（推荐）：用 winget 安装 Node.js LTS

在 PowerShell 执行：

```powershell
winget --version
```

如果能输出版本号，说明你有 winget，可以继续。

然后安装 Node.js LTS：

```powershell
winget install OpenJS.NodeJS.LTS
```

安装完成后，**关掉当前 PowerShell 窗口，再重新打开一个新的 PowerShell**（这一步很重要，很多“找不到命令”就卡在这里）。

再验证一次：

```powershell
node -v
npm -v
```

## 3.2 方法 B：去 Node.js 官网下载安装包

如果你的 `winget` 不可用（比如公司电脑禁用），就走官网安装：

- 选择 **LTS**（长期支持版），别选 Current（新特性多但更容易踩坑）
- 安装过程中保持默认选项即可（尤其是“Add to PATH”要勾上）

装完同样要重新打开 PowerShell，再用 `node -v`/`npm -v` 验证。

---

# 4. 安装 Codex CLI

## 4.1 全局安装（推荐）

在 PowerShell 执行：

```powershell
npm install -g @openai/codex
```

安装完成后验证：

```powershell
codex --version
```

如果输出了版本号，说明安装成功。

> 下面这张图是“成功时你大概会看到什么”的对照（输出可能不同，以你机器为准）。
>
> ![验证安装成功示例](images/Windows安装Codex安装教程/03-验证安装.png)

## 4.2 如果你遇到权限问题（常见）

如果安装时提示权限不足（比如写入某个全局目录被拒绝），优先按这个顺序尝试：

1. 关闭 PowerShell，用“**以管理员身份运行**”重新打开，再执行安装命令
2. 或者改用 Node.js 的默认设置（重新安装 Node.js，确保 npm 全局目录可写）

不建议新手一上来就改 npm 的全局目录/权限策略（容易越改越乱），先用管理员方式跑通更稳。

---

# 5. 首次运行：登录 / 配置 API Key（二选一）

先在 PowerShell 里运行：

```powershell
codex
```

通常会进入交互式引导：可能会提示你登录、授权、选择一些设置等。你按提示一步步做就行。

## 5.1 方式 A：按引导用账号登录（更适合新手）

优点：不用手动管理 API Key；更贴近“打开就用”的体验。
缺点：公司网络可能会拦截浏览器跳转/登录页。

遇到浏览器打不开时，先看第 7 章 FAQ。

## 5.2 方式 B：使用 API Key（更适合开发者/自动化）

如果你手里有 OpenAI API Key（形如 `sk-...`），可以先临时设置环境变量：

```powershell
$env:OPENAI_API_KEY="把你的 API Key 粘贴在这里"
codex
```

注意：上面这种写法**只在当前 PowerShell 窗口生效**。想要“重启电脑也不丢”，用 `setx` 写入用户环境变量：

```powershell
setx OPENAI_API_KEY "把你的 API Key 粘贴在这里"
```

然后**重新打开一个新的 PowerShell**，再确认：

```powershell
echo $env:OPENAI_API_KEY
```

> 安全提醒：API Key 是敏感信息，不要截图发群，不要写进代码仓库，不要提交到 Git。

## 5.3 方式 C: 使用 CC-Switch

参见  [CC-Switch使用教程.md](./CC-Switch使用教程.md)

---

# 6. 在你的项目里用 Codex（最常用的 3 个动作）

Codex 最好在“你的项目目录”里运行，这样它才能读到你的代码结构。

## 6.1 进入项目目录

举例：你的项目在 `D:\GithubCode\my-project`：

```powershell
cd D:\GithubCode\my-project
```

## 6.2 启动 Codex

```powershell
codex
```

你可以像聊天一样输入需求，例如：

- “帮我解释一下这个项目是干什么的，并给出运行步骤”
- “请找到导致报错的原因，并给出最小改动的修复方案”
- “帮我给这个函数补单元测试”

## 6.3 查看帮助（不会就看它）

```powershell
codex --help
```

---

# 7. FAQ（常见问题与排查）

## 7.1 运行 `codex` 提示“不是内部或外部命令”

优先按下面顺序排查：

1. 先确认真的装过：

   ```powershell
   npm list -g --depth=0
   ```

   看列表里有没有 `@openai/codex`。
2. 重新开一个新的 PowerShell（很多 PATH 问题就靠这一步解决）。
3. 看看 npm 的全局 bin 目录是否在 PATH：

   ```powershell
   npm config get prefix
   ```

   通常会对应一个目录，`codex` 会在它的子目录里。

## 7.2 `npm install -g @openai/codex` 安装失败，提示权限/EPERM

常用解决方式：

- 用管理员 PowerShell 重试一次
- 确认杀毒软件/安全策略没有拦截（公司电脑常见）

## 7.3 安装时提示需要编译工具（node-gyp / Python / VS Build Tools）

这通常不是 Codex 本身的问题，而是某些依赖需要本地编译环境。你可以：

1. 先升级到较新的 Node.js LTS
2. 再重试安装
3. 仍失败：安装 **Visual Studio Build Tools**（C++ 构建工具）

> 新手建议：优先用“最新 Node.js LTS + 管理员 PowerShell”组合，很多编译报错会直接消失。

## 7.4 公司网络登录/拉取失败（代理/证书）

现象可能是：

- 登录页面打不开
- 请求超时
- TLS/证书错误

建议做法：

1. 先确认浏览器能正常打开 OpenAI 相关页面
2. 如果公司需要代理，让 IT 给你正确的代理地址
3. 尽量不要用“跳过证书校验”这种危险方案

## 7.5 想升级 / 想卸载

升级：

```powershell
npm update -g @openai/codex
codex --version
```

卸载：

```powershell
npm uninstall -g @openai/codex
```

## 7.6 `winget` 不存在/不可用怎么办？

你执行 `winget --version` 如果提示找不到命令，常见原因是系统缺少“应用安装程序（App Installer）”或版本较旧。

新手最省事的做法是：**直接改走第 3.2 节（Node.js 官网安装包）**，不纠结 winget。

---

# 8. 参考资料（建议收藏）

官方文档（推荐以它为准）：

- OpenAI：Codex CLI（安装与使用）：https://developers.openai.com/codex/cli
- OpenAI：Codex 在 Windows 上的说明：https://developers.openai.com/codex/windows

---

# 9. 术语解释（文章里出现的“专业词”都在这里）

- **Codex CLI**：在命令行（终端）里运行的 Codex 工具，能读写本地项目并协助编程。
- **CLI（Command Line Interface）**：命令行界面，靠敲命令来操作的软件使用方式。
- **Node.js**：一个运行 JavaScript 的运行时环境；很多前端/工具链会依赖它。
- **npm**：Node.js 的包管理器，用来安装/升级命令行工具与依赖。
- **LTS（Long-Term Support）**：长期支持版本，更稳定，适合新手与生产环境。
- **winget**：Windows 的包管理工具，可以用命令安装/升级软件。
- **PowerShell**：Windows 自带的命令行工具（终端之一），本文所有命令都以它为例。
- **Windows Terminal**：微软提供的更现代的终端应用，可以同时开多个标签页（PowerShell/cmd 等）。
- **PATH**：系统环境变量之一，决定了你在终端里输入命令时，系统去哪些目录找可执行文件。
- **环境变量**：系统里的一些“全局配置键值”，程序可以读取它来决定如何运行（比如读取 `OPENAI_API_KEY`）。
- **API Key**：访问 API 的密钥，相当于“账号密码级别”的敏感信息。
- **沙箱（Sandbox）**：一种限制程序权限/行为的隔离环境，用来提升安全性，但也可能带来兼容性限制。
