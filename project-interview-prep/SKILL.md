---
name: project-interview-prep
description: Build evidence-grounded project retrospectives, resume material, and interview preparation only when the user explicitly says “请进行项目面试阶段” or invokes $project-interview-prep.
metadata:
  short-description: Project resume and interview preparation
---

# Project interview preparation

This skill is an explicit, menu-driven workflow. Do not activate it for ordinary coding, project completion, or casual discussion. Activate it only when the user explicitly writes:

```text
请进行项目面试阶段
```

or explicitly invokes `$project-interview-prep`.

## First response: show the menu only

When triggered, do not immediately write a full review or resume. First show the following selectable steps and wait for the user's choice:

```text
请选择要进行的项目面试步骤：

1. 项目背景、目标和最终效果
2. 技术栈、架构和个人负责范围
3. 项目痛点、原始方案和限制
4. 技术优化过程及优化前后数据
5. 项目简历描述
6. 面试口述版本（STAR/CAR 结构）
7. 面试官追问和参考回答
8. 证据缺口与需要补充的信息

可输入：
- 全部
- 1,3,4
- 只做简历描述
- 只分析某个模块
```

Do not execute any selected step until the user chooses. Preserve the selected order unless a prerequisite is missing.

## Step dependencies

- Steps 1 and 2 establish project context and ownership.
- Steps 3 and 4 establish the technical evidence chain.
- Steps 5 and 6 can use steps 1–4; if information is missing, request only the missing facts.
- Step 7 should be based on the selected project facts and should distinguish confirmed facts from likely follow-up questions.
- Step 8 can be run at any time and should list missing metrics, unclear ownership, and unsupported claims.

If the user selects “全部”, run the steps in numerical order. If a selected step depends on missing information, pause and ask a concise, focused question before continuing.

## Evidence-grounded project analysis

Build every technical story using this chain:

```text
Project context and goal
→ original approach
→ observed pain point
→ evidence of the pain
→ chosen technical approach
→ concrete implementation changes
→ before/after comparison
→ trade-offs and remaining limitations
```

For every result:

- Separate the user's own contribution from team contributions.
- Prefer measured before/after values.
- Record the test environment, dataset or traffic, sample size, and time window when available.
- If a value is missing, write “未记录” and identify how it could be measured.
- Mark estimates as “估算” and state their basis.
- Never invent performance numbers, business impact, user counts, or responsibilities.
- Distinguish directly verified facts, user-provided claims, estimates, and reasonable inferences.

## Technical stack and optimization analysis

Explain why a technology was selected and what pain point it addressed. When comparing alternatives, consider:

- Fit with the existing project.
- Implementation and migration cost.
- Runtime or operational cost.
- Maintenance activity and documentation.
- License and dependency risk.
- Performance, reliability, and scalability trade-offs.

Do not search for or propose technologies unrelated to the selected project or module.

## Output formats

When the user selects a step, produce only that step's output unless they ask for more. Use these formats where applicable:

### Resume description

Provide concise versions suitable for:

- One-line project summary.
- Chinese resume bullet points.
- English resume bullet points when requested.
- A version emphasizing technical depth.
- A version emphasizing measurable impact.

Do not add unsupported metrics or inflate the user's role.

### Interview explanation

Use a clear narrative:

```text
项目背景 → 我的职责 → 主要难点 → 技术方案 → 关键取舍 → 最终效果 → 复盘
```

Keep the spoken version natural and concise, then provide deeper detail for likely follow-up questions.

### Interview questions

Generate questions in groups:

- Project background and ownership.
- Architecture and technology choices.
- Pain points and optimization evidence.
- Failure cases and trade-offs.
- Testing, monitoring, and reliability.
- Future improvements.

For each question, provide a fact-grounded answer outline. Mark any answer that needs user confirmation.

## Completion

End the selected step with:

- Facts used.
- Assumptions or estimates.
- Missing evidence.
- The next available step from the menu.

This skill does not modify source code, run Git operations, or deploy systems.
