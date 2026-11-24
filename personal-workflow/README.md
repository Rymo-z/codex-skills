# Personal Workflow

这个 Skill 用于执行用户偏好的开发工作流，覆盖需求分析、技术选型、模块化实现、验证以及 Git 交付。

## 核心流程

1. 先只读分析需求和现有实现；“排查一下”“是否需要修改”等问题只输出分析和方案
2. 开始修改前，说明改哪些文件或模块、怎么改、预期效果和验证方法，等待用户确认；小改动也适用
3. 方案确认后，连续完成范围内所有模块、测试和必要修复，不因换模块、换文件或测试失败反复询问
4. 先复用项目已有代码和依赖，必要时再评估外部方案
5. 开发过程中记录技术决策、个人贡献和真实验证数据
6. 缺少权限、依赖或业务决策时暂停询问
7. 提交前检查分支、远端更新、冲突和文件归属，只提交当前任务文件

确认边界是已确认的方案范围。只确认需求、不确认具体实施方案时，仍须先给出方案；方案确认后直接改完并测试完。只有超出范围、实质改变方案、出现新的关键决策，或触及依赖安装、生产操作等单独授权规则时，才再次询问。

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
