# Codex Skills

这是 Rymo-z 的个人 Codex Skills 仓库。

## 包含内容

- [karpathy-guidelines](./karpathy-guidelines)：简单、谨慎、目标驱动的代码工作规范。
- [personal-workflow](./personal-workflow)：需求分析、技术选型、模块化开发、证据记录、验证和 Git 交付流程。
- [project-interview-prep](./project-interview-prep)：项目复盘、简历描述和面试准备。

## 下载和安装

### 下载整个仓库

```powershell
git clone https://github.com/Rymo-z/codex-skills.git
```

然后复制需要的 Skill：

```powershell
Copy-Item -Recurse -Force .\codex-skills\karpathy-guidelines C:\Users\<用户名>\.codex\skills\karpathy-guidelines
Copy-Item -Recurse -Force .\codex-skills\personal-workflow C:\Users\<用户名>\.codex\skills\personal-workflow
Copy-Item -Recurse -Force .\codex-skills\project-interview-prep C:\Users\<用户名>\.codex\skills\project-interview-prep
```

### 只下载单个 Skill

- [karpathy-guidelines/SKILL.md](https://raw.githubusercontent.com/Rymo-z/codex-skills/main/karpathy-guidelines/SKILL.md)
- [personal-workflow/SKILL.md](https://raw.githubusercontent.com/Rymo-z/codex-skills/main/personal-workflow/SKILL.md)
- [project-interview-prep/SKILL.md](https://raw.githubusercontent.com/Rymo-z/codex-skills/main/project-interview-prep/SKILL.md)

下载后分别保存到：

```text
C:\Users\<用户名>\.codex\skills\karpathy-guidelines\SKILL.md
C:\Users\<用户名>\.codex\skills\personal-workflow\SKILL.md
C:\Users\<用户名>\.codex\skills\project-interview-prep\SKILL.md
```

## 说明

Skill 文件需要放在对应目录中，Codex 才能按名称发现。修改 Skill 后，重新打开相关任务或重新加载 Skills 即可使用最新内容。
