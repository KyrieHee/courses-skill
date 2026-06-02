---
name: course-learning-orchestrator
description: Orchestrate course learning workflows for K-12 and university courses. Use when the user provides a course target such as "初一语文人教版", "高中数学必修一", "大学线性代数", "AP Biology", textbook edition, grade, semester, unit, exam goal, or asks for a full study plan that should route to diagnosis, preview, tutoring, practice, review, exam prep, mistake notebook, reflection, and synthesis skills.
---

# Course Learning Orchestrator

## Overview

Use this skill as the controller for structured course learning. It parses the learner's course context, identifies missing inputs, chooses the right stage skills, and produces a learning plan that can be handed off stage by stage.

Inspired by multi-skill orchestration patterns: keep the controller lean, create explicit stage contracts, and make each downstream skill produce a handoff artifact.

## Skill Map

- `course-diagnosis`: determine learner baseline, goals, constraints, prerequisites, and risk points.
- `course-preview`: produce lesson/unit previews before class or self-study.
- `course-tutoring`: explain concepts, texts, examples, problem-solving methods, and university-level theory.
- `course-practice`: generate homework, drills, reading tasks, recitation, lab, essay, or problem sets.
- `course-review`: consolidate knowledge after class, unit study, or chapter completion.
- `course-exam`: prepare for quizzes, midterms, finals, entrance exams, placement tests, or certification exams.
- `course-mistake-notebook`: classify wrong answers, diagnose causes, and schedule targeted repair.
- `course-reflection`: run learning retrospectives, habit review, strategy adjustment, and metacognitive checks.
- `course-synthesis`: combine all stage artifacts into a full plan, weekly calendar, progress dashboard, or final study report.

## Default Pipeline

1. Parse course request: education stage, grade/year, subject, textbook/version, semester, unit/chapter, learner level, goal, deadline, available time, and assessment type.
2. Diagnose: if baseline, goal, or constraints are unclear, run `course-diagnosis` or ask only the minimum clarifying questions.
3. Align content: infer likely curriculum scope, but verify or ask for textbook table of contents when exact unit content matters.
4. Plan preview: run `course-preview` for upcoming lessons, key terms, reading, prerequisite refresh, and questions to bring to class.
5. Teach and practice: use `course-tutoring` for explanation and `course-practice` for output tasks and drills.
6. Review: run `course-review` after study sessions, lessons, or units.
7. Exam prep: run `course-exam` when there is a test target or when the user asks for scoring improvement.
8. Mistake repair: run `course-mistake-notebook` whenever the user provides wrong answers, weak points, or test papers.
9. Reflection: run `course-reflection` after a cycle, exam, project, or when motivation/time management is a problem.
10. Synthesize: run `course-synthesis` to produce the final learning plan and next actions.

## Routing Rules

- If the user says only a course, for example "中学初一语文人教版", create a starter plan and state missing assumptions: semester, current unit, learner level, exam date, weekly time.
- If the course is Chinese K-12 "语文", treat "人教版" and "统编版/部编版" carefully; ask or verify when unit texts or exam requirements depend on the exact edition and year.
- If the user provides a textbook chapter, course syllabus, slides, homework, exam paper, or table of contents, ground the plan in that artifact.
- If the user asks "预习", "课前", or "下一课", route to `course-preview`.
- If the user asks "讲一下", "看不懂", "例题", "文本解读", or "证明", route to `course-tutoring`.
- If the user asks "作业", "练习", "背诵", "刷题", "论文", "实验", or "项目", route to `course-practice`.
- If the user asks "复习", "知识点", "总结", "导图", or "查漏补缺", route to `course-review`.
- If the user asks "考试", "期中", "期末", "中考", "高考", "考研", "quiz", "midterm", or "final", route to `course-exam`.
- If the user provides wrong answers, lost-score notes, essay feedback, test-paper photos, or homework feedback, route to `course-mistake-notebook`.
- If the user asks "复盘", "为什么没学会", "怎么坚持", "学习方法", or "时间安排", route to `course-reflection`.
- If the user asks for "完整计划", "学习规划", "综合方案", "一周安排", or "学期规划", route to `course-synthesis` after diagnosis.

## Planning Principles

- Match grade level and subject style. K-12 plans should be concrete, scaffolded, and parent/teacher friendly; university plans can include prerequisites, readings, problem sets, office-hour questions, and project milestones.
- Separate curriculum facts from assumptions. Verify current syllabi, textbook editions, exam policies, and local requirements when they may have changed.
- Preserve learner agency: provide choices, checkpoints, and self-test prompts instead of only assigning tasks.
- Include retrieval practice, spaced review, worked examples, deliberate practice, feedback loops, and mistake repair.
- For language and humanities, include reading, annotation, expression, writing, recitation, discussion, and transfer tasks.
- For STEM, include prerequisites, concepts, worked examples, problem types, derivations, applications, and cumulative mixed practice.
- For university courses, include lecture alignment, reading notes, problem sets, labs/projects, grading rubric, and office-hour preparation.

## Quality Gates

Do not finalize a plan when:

- Grade/course, subject, edition, or target scope is ambiguous and would change content materially.
- The plan contains textbook-specific claims without source material or confidence labeling.
- Tasks are too broad to execute in a single study session.
- Exam preparation lacks scoring criteria, sample questions, timing, or error analysis.
- Review lacks active recall or spaced repetition.
- Mistake work records only the right answer without root cause and transfer practice.
- The final plan does not include checkpoints, time budget, and next action.

## Output

Return:

- Parsed course profile and assumptions.
- Recommended pipeline and skipped stages.
- Missing inputs, if any.
- Immediate starter plan for the next 3-7 days.
- Stage-by-stage handoff briefs.
- Final deliverable format: daily plan, weekly plan, unit plan, exam sprint, or semester roadmap.

## Resources

Read `references/workflow-control.md` for stage contracts, handoff templates, and final plan formats.
