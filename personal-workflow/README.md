# Personal Workflow

这个 Skill 用于执行用户偏好的开发工作流，覆盖需求分析、技术选型、模块化实现、验证以及 Git 交付。

## 核心流程

1. 判断任务复杂度，选择轻量或完整流程
2. 澄清阻塞性需求，记录非阻塞默认假设
3. 先检查项目已有代码和依赖，再评估外部方案
4. 按模块实现，每个模块定义完成标准和验证命令
5. 缺少权限、依赖或业务决策时暂停询问
6. 提交前检查分支、远端更新、冲突和文件归属
7. 只提交当前任务文件，推送工作分支

## 在 Codex 中安装

将当前目录复制到 Codex 的个人 Skills 目录：

```powershell
Copy-Item -Recurse -Force .\personal-workflow C:\Users\<用户名>\.codex\skills\personal-workflow
```

Windows 当前用户的默认安装路径是：

```text
C:\Users\<用户名>\.codex\skills\personal-workflow\SKILL.md
```

## 从 GitHub 下载

```powershell
git clone https://github.com/Rymo-z/codex-skills.git
Copy-Item -Recurse -Force .\codex-skills\personal-workflow C:\Users\<用户名>\.codex\skills\personal-workflow
```

也可以只下载文件：

[下载 SKILL.md](https://raw.githubusercontent.com/Rymo-z/codex-skills/main/personal-workflow/SKILL.md)

## 使用方式

这个 Skill 适用于代码开发、审查、测试、提交、推送和部署相关任务。通常会由 Codex 根据任务自动识别，也可以明确写：

```text
请使用 $personal-workflow 执行这个任务。
```

它会与 `karpathy-guidelines` 和 `engineering-constraints` 配合使用，不替代系统、开发者或当前用户指令。
