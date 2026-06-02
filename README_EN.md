# Course Learning Skills

A Codex skill suite for K-12 and university course learning. When a user enters a course target such as "Grade 7 Chinese, Renmin Education Press", "High School Math Compulsory 1", or "University Linear Algebra final review", `course-learning-orchestrator` parses the learning context and routes the task to diagnosis, preview, tutoring, practice, review, exam prep, mistake repair, reflection, and synthesis skills.

This project follows the orchestrator-style skill organization inspired by [alchaincyf/nuwa-skill](https://github.com/alchaincyf/nuwa-skill): one controller identifies the entry point, routes stages, preserves intermediate artifacts, and makes each downstream skill return a handoff-ready output.

Chinese version: [README.md](README.md)

## What It Does

- Supports learning plans for primary school, middle school, high school, and university courses.
- Accepts different entry points: textbook edition, grade, subject, chapter, exam goal, homework, essays, and wrong answers.
- Starts from vague prompts such as "Grade 7 Chinese, Renmin Education Press" by creating a course profile, identifying missing inputs, and producing a starter plan.
- Breaks learning into reusable stages: diagnosis, preview, tutoring, practice, review, exam prep, mistake notebook, reflection, and synthesis.
- Adapts to language arts, math/STEM, humanities, social sciences, university courses, labs, projects, and papers.

## Installation And Deployment

### Option 1: Copy all course skills into local Codex skills

Run this from the repository root:

```bash
mkdir -p ~/.codex/skills
cp -R course-* ~/.codex/skills/
```

Then restart Codex or refresh the skill list. You can invoke the skills with names such as `$course-learning-orchestrator`.

### Option 2: Install only the course learning skills

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

### Verify Installation

```bash
ls ~/.codex/skills/course-learning-orchestrator
ls ~/.codex/skills/course-preview
```

If you see `SKILL.md` and `agents/openai.yaml`, the directory structure is ready.

### Update Deployment

When the repository skills are updated, copy them again:

```bash
cp -R course-* ~/.codex/skills/
```

## Skill Map And Examples

| Skill | Purpose | Example |
| --- | --- | --- |
| `course-learning-orchestrator` | Main controller that parses the course request and routes later stages | `Use $course-learning-orchestrator to create a 4-week study plan for Grade 7 Chinese.` |
| `course-diagnosis` | Diagnoses baseline, goals, weak points, and constraints | `Use $course-diagnosis to diagnose why my Grade 7 Chinese reading comprehension keeps losing points.` |
| `course-preview` | Creates pre-class previews, guiding questions, and self-checks | `Use $course-preview to preview the next Grade 7 Chinese text before class.` |
| `course-tutoring` | Explains concepts, texts, examples, proofs, writing, and projects | `Use $course-tutoring to explain the main idea and writing techniques of this text.` |
| `course-practice` | Generates homework, drills, problem sets, recitation tasks, essays, and rubrics | `Use $course-practice to generate reading comprehension drills for Grade 7 Chinese.` |
| `course-review` | Builds knowledge maps, active recall prompts, spaced review, and gap checks | `Use $course-review to turn this week's Chinese notes into an active recall plan.` |
| `course-exam` | Creates prep plans for quizzes, midterms, finals, and major exams | `Use $course-exam to prepare for my Grade 7 Chinese midterm in 14 days.` |
| `course-mistake-notebook` | Analyzes wrong answers, root causes, transfer drills, and recheck schedules | `Use $course-mistake-notebook to analyze these reading comprehension mistakes.` |
| `course-reflection` | Reviews study cycles, methods, time use, and motivation | `Use $course-reflection to review why last week's study plan was not completed.` |
| `course-synthesis` | Combines stage artifacts into a complete study plan | `Use $course-synthesis to combine my diagnosis, practice results, and exam goal into a weekly plan.` |

## Example

User input:

```text
Grade 7 Chinese, Renmin Education Press. Help me create a learning plan.
```

Recommended invocation:

```text
Use $course-learning-orchestrator to build a full course learning plan for Grade 7 Chinese.
```

The orchestrator will return:

- Course profile: Grade 7, Chinese, textbook edition pending confirmation.
- Key missing inputs: current semester, current unit, exam or improvement goal, weekly study time.
- A 7-day starter plan: diagnosis, current text preview, reading annotation, vocabulary and recitation, reading comprehension, writing practice, review and mistake repair.
- Handoffs: route to `course-preview` for pre-class guidance, `course-review` for unit review, `course-exam` for exam sprints, and `course-mistake-notebook` for wrong-answer repair.

## Workflow

Default learning loop:

1. Parse the course request: grade, subject, textbook, chapter, goal, time budget, and assessment type.
2. Diagnose: identify baseline, weak points, goals, and constraints.
3. Align content: use textbook tables of contents, syllabi, lecture notes, homework, or exam scope when available.
4. Preview: build keywords, background knowledge, guiding questions, and quick self-checks.
5. Tutor: explain concepts, texts, examples, proofs, or methods.
6. Practice: generate leveled drills, writing tasks, reading tasks, or project steps.
7. Review: create knowledge maps, active recall prompts, mixed practice, and spaced review.
8. Exam prep: prioritize high-yield topics, timed practice, mock tests, and test-day strategy.
9. Mistake repair: classify causes, rewrite methods, create transfer drills, and schedule rechecks.
10. Reflection: review what worked, adjust strategy, and define the next learning experiment.
11. Synthesis: produce a weekly plan, unit roadmap, exam sprint, or semester plan.

## Repository Structure

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

Each skill directory includes:

- `SKILL.md`: trigger conditions, workflow, rules, and output format.
- `agents/openai.yaml`: display name, short description, and default invocation prompt.

The orchestrator directory also includes:

- `references/workflow-control.md`: course profile schema, stage handoff templates, and starter plan format.

## Usage Patterns

Full plan:

```text
Use $course-learning-orchestrator to create a 4-week study plan for High School Math Compulsory 1.
```

Pre-class preview:

```text
Use $course-preview to preview the next Grade 7 Chinese text.
```

Exam sprint:

```text
Use $course-exam to prepare for my university linear algebra final in 10 days.
```

Mistake repair:

```text
Use $course-mistake-notebook to analyze these wrong answers and create transfer drills.
```

Reflection:

```text
Use $course-reflection to review why last week's study plan failed and adjust the next cycle.
```

## Design Principles

- Diagnose before planning. Do not assign a large task list before the learner's baseline, goals, and time budget are clear.
- Make every stage handoff-ready so preview can flow into review, mistakes can flow into exam prep, and reflection can flow into synthesis.
- Keep tasks executable. Each study block should include time, method, output evidence, and a checkpoint.
- Prefer active learning: retrieval practice, spaced repetition, transfer practice, root-cause mistake analysis, and feedback loops.
- Adapt by education stage. K-12 plans should include scaffolding, textbooks, exams, and parent/teacher support; university plans should include prerequisites, lectures, readings, assignments, projects, grading weights, and office hours.
- Label uncertainty honestly. Textbook editions, local exam policies, course syllabi, and textbook content can change, so ask for tables of contents, syllabi, papers, or teacher requirements when exact content matters.

## Boundaries

These skills help generate learning plans, practice tasks, review paths, and mistake repair strategies, but they do not replace formal teacher plans, school exam instructions, or current textbook information. For exact textbook texts, local exam policies, university grading policies, or current syllabi, rely on user-provided materials or reliable sources.

## Suggested First Prompt

```text
Use $course-learning-orchestrator to create a course learning plan for Grade 7 Chinese. Assume the learner has 5 hours per week, wants to improve reading comprehension and writing, and has a unit test in 3 weeks.
```
