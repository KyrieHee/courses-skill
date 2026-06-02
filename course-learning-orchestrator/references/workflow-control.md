# Course Workflow Control

## Course Profile Schema

Use this schema in handoffs:

- Education stage: primary, middle school, high school, undergraduate, graduate, professional, or unknown.
- Grade/year: for example 小学五年级, 初一/七年级, 高二, 大一.
- Subject/course: for example 语文, 数学, English, Calculus, Linear Algebra.
- Curriculum/textbook: publisher, edition, semester, required/elective, syllabus, instructor notes.
- Scope: whole semester, unit, chapter, lesson, text, problem set, exam range.
- Learner baseline: strengths, weak points, prior knowledge, language level, confidence.
- Goal: preview, catch up, improve score, pass exam, deepen understanding, project completion.
- Constraints: deadline, weekly time, tools, class schedule, parent/teacher involvement.
- Assessment: quiz, homework, essay, oral presentation, lab, midterm, final, standardized exam.

## Stage Contracts

### Diagnosis Handoff

Input:

- Course profile.
- Learner self-report, recent scores, wrong answers, teacher comments, or sample work if available.

Output:

- Baseline level.
- Prerequisite gaps.
- High-risk topics.
- Learning goal and success metrics.
- Recommended stage sequence.

### Preview Handoff

Input:

- Course profile.
- Upcoming lesson/unit/chapter.
- Time available before class.

Output:

- Preview objective.
- Must-know vocabulary/concepts.
- Reading or example walkthrough.
- 3-5 guiding questions.
- Quick self-check.
- Questions to ask teacher/tutor.

### Tutoring Handoff

Input:

- Concept/text/problem to explain.
- Learner baseline and confusion point.

Output:

- Plain-language explanation.
- Key structure or method.
- Worked example or close reading.
- Common misconceptions.
- Short transfer task.

### Practice Handoff

Input:

- Topic, goal, difficulty, desired volume, and available time.

Output:

- Practice set by level.
- Answer key or rubric.
- Timing suggestion.
- Error logging fields.
- Extension task.

### Review Handoff

Input:

- Completed lesson/unit and notes.
- Weak points or practice results.

Output:

- Knowledge map.
- Retrieval prompts.
- Mixed review tasks.
- Spaced repetition schedule.
- Remaining gaps.

### Exam Handoff

Input:

- Exam date, scope, format, score goal, current score, and sample papers if available.

Output:

- Score gap diagnosis.
- High-yield topic list.
- Timed practice plan.
- Mock test schedule.
- Test-taking strategy.
- Final 24-hour plan.

### Mistake Notebook Handoff

Input:

- Wrong answers, original question, student solution, correct answer, score/rubric if available.

Output:

- Mistake category.
- Root cause.
- Correct solution path.
- Similar transfer drills.
- Recheck schedule.
- Rule/pattern to remember.

### Reflection Handoff

Input:

- Recent study cycle, plan completion, emotional/motivation notes, scores, and bottlenecks.

Output:

- What worked.
- What failed and why.
- Strategy adjustment.
- Habit or environment fix.
- Next experiment.

### Synthesis Handoff

Input:

- Course profile and all available stage outputs.

Output:

- Executive summary for learner/parent/teacher.
- Priority learning goals.
- Calendar plan.
- Stage tasks.
- Checkpoints.
- Risk controls.
- Next action.

## Starter Plan Format

For a vague request such as "初一语文人教版", return:

1. Parsed profile and assumptions.
2. Missing questions, limited to the 3 most important.
3. A conservative 7-day starter plan:
   - Day 1: diagnosis and textbook alignment.
   - Day 2: preview current unit/text.
   - Day 3: guided reading and annotation.
   - Day 4: vocabulary, recitation, and expression practice.
   - Day 5: reading comprehension drills.
   - Day 6: writing or language-use practice.
   - Day 7: review, mistake repair, and reflection.
4. Handoff briefs for preview, review, exam prep, mistake notebook, and synthesis.

## Final Plan Format

Use concise tables when helpful:

- Goal.
- Task.
- Time.
- Method.
- Output evidence.
- Checkpoint.

Always include:

- First action the learner can do today.
- How progress will be measured.
- When to revisit the plan.
