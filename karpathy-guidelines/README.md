# Karpathy Guidelines

这个 Skill 用于减少 AI 在写代码时的常见问题，适合代码开发、审查和重构。

## 解决的问题

- 避免在需求不清楚时擅自猜测
- 优先采用简单、足够的实现
- 只修改与当前任务直接相关的代码
- 用明确的成功标准和验证结果闭环

## 在 Codex 中安装

将当前目录复制到 Codex 的个人 Skills 目录：

```powershell
Copy-Item -Recurse -Force .\karpathy-guidelines C:\Users\<用户名>\.codex\skills\karpathy-guidelines
```

Windows 当前用户的默认安装路径是：

```text
C:\Users\<用户名>\.codex\skills\karpathy-guidelines\SKILL.md
```

## 从 GitHub 下载

```powershell
git clone https://github.com/Rymo-z/codex-skills.git
Copy-Item -Recurse -Force .\codex-skills\karpathy-guidelines C:\Users\<用户名>\.codex\skills\karpathy-guidelines
```

也可以只下载文件：

[下载 SKILL.md](https://raw.githubusercontent.com/Rymo-z/codex-skills/main/karpathy-guidelines/SKILL.md)

## 使用方式

通常会由 Codex 根据任务自动识别。也可以在请求中明确写：

```text
请使用 $karpathy-guidelines 完成这个代码任务。
```

这个 Skill 不负责项目特定的 Git 流程、部署流程或个人工作习惯。
