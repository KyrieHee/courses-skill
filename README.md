# Course Learning Skills

面向中小学与大学课程学习的 Codex skill 套件。用户只要输入类似“初一语文人教版”“高中数学必修一”“大学线性代数期末复习”这样的课程目标，`course-learning-orchestrator` 会先解析学习场景，再按需调用诊断、预习、讲解、练习、复习、考试、错题、复盘和综合规划等子技能，生成可执行的学习路径。

这个项目参考了 [alchaincyf/nuwa-skill](https://github.com/alchaincyf/nuwa-skill) 的总控式 skill 组织思路：用一个 orchestrator 识别任务入口、分派阶段、沉淀中间产物，并让每个子 skill 输出可交接的结果。

English version: [README_EN.md](README_EN.md)

## 功能概览

- 支持小学、初中、高中、大学课程学习规划。
- 支持教材版本、年级、学科、章节、考试目标、作业和错题等不同入口。
- 能从模糊输入开始，例如“中学初一语文人教版”，先做课程画像和缺失信息判断，再给出 starter plan。
- 将学习流程拆成可复用阶段：诊断、预习、讲解、练习、复习、考试、错题、复盘、综合规划。
- 适配不同学科：语文/英语、数学/STEM、人文社科、大学课程、实验/项目/论文类任务。

## 安装部署

### 方式一：复制到本地 Codex skills 目录

在本仓库根目录执行：

```bash
mkdir -p ~/.codex/skills
cp -R course-* ~/.codex/skills/
```

然后重启 Codex 或刷新 skill 列表，即可通过 `$course-learning-orchestrator` 等名称调用。

### 方式二：只安装课程学习相关 skill

```bash
mkdir -p ~/.codex/skills
cp -R course-learning-orchestrator ~/.codex/skills/
cp -R course-diagnosis ~/.codex/skills/
cp -R course-preview ~/.codex/skills/
cp -R course-tutoring ~/.codex/skills/
cp -R course-practice ~/.codex/skills/
cp -R course-review ~/.codex/skills/
cp -R course-exam ~/.codex/skills/
cp -R course-mistake-notebook ~/.codex/skills/
cp -R course-reflection ~/.codex/skills/
cp -R course-synthesis ~/.codex/skills/
```

### 验证安装

```bash
ls ~/.codex/skills/course-learning-orchestrator
ls ~/.codex/skills/course-preview
```

如果能看到 `SKILL.md` 和 `agents/openai.yaml`，说明目录结构已就绪。

### 更新部署

当本仓库 skill 有更新时，重新复制覆盖即可：

```bash
cp -R course-* ~/.codex/skills/
```

## Skill Map 与案例

| Skill | 用途 | 案例 |
| --- | --- | --- |
| `course-learning-orchestrator` | 课程学习总控，解析输入并编排后续阶段 | `使用 $course-learning-orchestrator 为初一语文人教版制定 4 周学习计划。` |
| `course-diagnosis` | 诊断学习起点、目标、薄弱点和约束 | `使用 $course-diagnosis 诊断我为什么七年级语文阅读理解总是丢分。` |
| `course-preview` | 生成课前预习、导学问题和自测 | `使用 $course-preview 为七年级语文《春》准备课前预习。` |
| `course-tutoring` | 讲解概念、课文、例题、证明、写作和项目 | `使用 $course-tutoring 讲解这篇课文的中心思想和写作手法。` |
| `course-practice` | 生成作业、训练、题组、背诵、作文和评分标准 | `使用 $course-practice 为初一语文生成阅读理解专项练习。` |
| `course-review` | 做知识梳理、主动回忆、间隔复习和查漏补缺 | `使用 $course-review 把本周语文笔记整理成主动回忆复习计划。` |
| `course-exam` | 制定测验、期中、期末和大考备考方案 | `使用 $course-exam 为 14 天后的七年级语文期中考试制定备考计划。` |
| `course-mistake-notebook` | 分析错题、归因、迁移训练和回查计划 | `使用 $course-mistake-notebook 分析这些阅读理解错题并生成迁移练习。` |
| `course-reflection` | 复盘学习周期、方法、时间和动机问题 | `使用 $course-reflection 复盘为什么上周学习计划没有完成。` |
| `course-synthesis` | 将各阶段结果整合为完整学习规划 | `使用 $course-synthesis 把诊断结果、练习反馈和考试目标整合成一份周计划。` |

## 示例

用户输入：

```text
中学初一语文人教版，帮我做一个学习规划
```

推荐调用：

```text
使用 $course-learning-orchestrator 为初一语文人教版生成完整学习规划。
```

总控会输出：

- 课程画像：初一/七年级、语文、教材版本待确认、可能为统编版/人教相关版本。
- 关键缺失信息：当前学期、正在学哪一单元、考试或提升目标、每周可学习时间。
- 7 天 starter plan：诊断教材与基础、预习当前课文、阅读批注、字词背诵、阅读理解、写作训练、复习和错题修复。
- 后续 handoff：交给 `course-preview` 做课前导学，交给 `course-review` 做单元复习，交给 `course-exam` 做考试冲刺，交给 `course-mistake-notebook` 处理错题。

## 工作流

默认学习闭环：

1. 解析课程请求：年级、学科、教材、章节、目标、时间和考试类型。
2. 课程诊断：判断基础、薄弱点、目标和约束。
3. 内容对齐：根据教材、目录、讲义、作业或考试范围确定学习内容。
4. 课前预习：建立关键词、背景知识、导学问题和自测。
5. 课程讲解：解释核心概念、文本、例题、证明或方法。
6. 针对练习：生成分层题组、写作任务、阅读任务或项目步骤。
7. 课后复习：知识图谱、主动回忆、混合练习和间隔复习。
8. 考试备考：高频考点、限时训练、模拟卷和考场策略。
9. 错题修复：分类错因、重写方法、迁移练习和回查安排。
10. 学习复盘：总结有效方法、调整计划、制定下一轮实验。
11. 综合规划：输出周计划、单元计划、考试冲刺或学期路线图。

## 目录结构

```text
.
├── README.md
├── README_EN.md
├── course-learning-orchestrator/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/workflow-control.md
├── course-diagnosis/
├── course-preview/
├── course-tutoring/
├── course-practice/
├── course-review/
├── course-exam/
├── course-mistake-notebook/
├── course-reflection/
└── course-synthesis/
```

每个 skill 目录都包含：

- `SKILL.md`：触发条件、工作流、规则和输出格式。
- `agents/openai.yaml`：界面展示名、简短描述和默认调用提示。

总控目录额外包含：

- `references/workflow-control.md`：课程画像 schema、阶段 handoff 模板和 starter plan 格式。

## 使用场景

完整规划：

```text
使用 $course-learning-orchestrator 为高一数学必修一制定 4 周学习计划。
```

课前预习：

```text
使用 $course-preview 为七年级语文《春》做课前预习。
```

考试冲刺：

```text
使用 $course-exam 为 10 天后的大学线性代数期末考试制定冲刺计划。
```

错题修复：

```text
使用 $course-mistake-notebook 分析这些错题，并生成同类迁移练习。
```

复盘调整：

```text
使用 $course-reflection 复盘上周学习计划为什么没有完成，并调整下一轮安排。
```

## 设计原则

- 先诊断，再规划。不要在学生基础、目标和时间不清楚时直接堆任务。
- 每个阶段都有 handoff，方便从预习接到复习、从错题接到考试、从复盘接到综合规划。
- 任务要可执行。每个学习块应该有时间、方法、产出证据和检查点。
- 主动学习优先。强调主动回忆、间隔复习、迁移练习、错题归因和反馈循环。
- 学段适配。中小学强调脚手架、教材、考试和家校协同；大学强调先修知识、讲义、阅读、作业、项目、评分权重和 office hours。
- 诚实标注不确定性。教材版本、地区考试政策、课程大纲和教材内容可能变化，必要时应要求用户提供目录、讲义、试卷或教师要求。

## 边界说明

这些 skills 可以帮助生成学习计划、练习、复习路径和错题修复策略，但不能替代教师的正式课程安排、学校考试说明或最新教材版本信息。凡是涉及具体教材篇目、地区考试政策、大学课程 grading policy、最新 syllabus 的内容，应以用户提供材料或可靠来源为准。

## 推荐首次调用

```text
使用 $course-learning-orchestrator 为初一语文人教版制定课程学习计划。假设学生每周有 5 小时学习时间，希望提升阅读理解和写作能力，并且 3 周后有一次单元测验。
```
