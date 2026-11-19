# Project Interview Prep

这个 Skill 用于把已完成的项目整理成简历材料、项目复盘和面试准备内容。

## 触发方式

它只在你明确输入下面的指令时启动：

```text
请进行项目面试阶段
```

也可以显式调用：

```text
$project-interview-prep
```

触发后会先展示步骤菜单，等待你选择，不会直接生成完整材料。

## 可选步骤

1. 项目背景、目标和最终效果
2. 技术栈、架构和个人负责范围
3. 项目痛点、原始方案和限制
4. 技术优化过程及优化前后数据
5. 项目简历描述
6. 面试口述版本
7. 面试官追问和参考回答
8. 证据缺口与需要补充的信息

可以输入 `全部`、`1,3,4`、`只做简历描述` 或指定某个模块。

## 证据要求

- 不编造性能指标、业务收益、用户数量或个人职责。
- 没有真实数据时标记为“未记录”。
- 估算数据必须标记“估算”并说明依据。
- 区分个人贡献和团队共同完成的工作。
- 技术难点按“原方案 → 痛点 → 优化 → 效果 → 代价”整理。

## 安装

```powershell
git clone https://github.com/Rymo-z/codex-skills.git
Copy-Item -Recurse -Force .\codex-skills\project-interview-prep C:\Users\<用户名>\.codex\skills\project-interview-prep
```

也可以直接下载 [SKILL.md](https://raw.githubusercontent.com/Rymo-z/codex-skills/main/project-interview-prep/SKILL.md)，保存到：

```text
C:\Users\<用户名>\.codex\skills\project-interview-prep\SKILL.md
```

这个 Skill 只生成复盘、简历和面试材料，不修改代码、不执行 Git 操作、不部署系统。
