---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer exactly this question for exactly one package per run: **is this
candidate pull request ready to submit?** Treat the package as its draft
title and description, commits, diff, and test evidence, read against
the plan it claims to implement and the issue that plan belongs to.
Assess readiness to open the PR, not whether it will be reviewed,
merged, or closed. Do not grade an unrelated artifact or answer a
different question.

## Inputs and modes

Run in exactly one of these modes:

- **Live mode:** After the scope check below, use the student's
  `plan.md`, including its deviation notes, as the implementation plan;
  obtain the candidate's issue from that plan and read its issue thread
  in the scoped repository. Read the student's draft PR title and
  description, test evidence, and the working copy's complete branch
  diff against the repository's default branch. The diff is produced
  from the working copy with `git diff main...HEAD` (three dots; use the
  scoped repository's actual default branch name if it is not `main`).
  Use the house plan and house reproduction pack instead of the
  student's `plan.md` and test evidence when the student is on the
  house chain; grade them against the same rubric. Gather issue-side
  evidence from the real repository, including the issue thread, PR
  template, and applicable stated policy.
- **Eval mode:** Treat the supplied package bundle as the complete
  world. Read every relevant fact from its text; do not fetch anything,
  inspect other files, or use outside knowledge to fill gaps. Run every
  rubric check and apply the complete verdict rule.

Do not silently substitute missing inputs. Follow `procedure.md` for
how to gather and record the evidence; if required evidence is absent
or unverifiable, grade the affected check as `unclear` unless the
rubric specifies otherwise.

## The scope seam (live mode only)

In live mode, read `scope.md` before any other package input or
repository evidence. Require its `Repo:` line to name the scoped
Path Review repository, and use the file's house rules when checking
the package. If the line is still a placeholder or otherwise
unfilled, stop without grading and tell the student to fill in the
`Repo:` line with their section's Path Review repository. If the
candidate targets a repository outside that scope, refuse to grade it.
Do not guess the intended repository or treat an out-of-scope package
as an eval bundle. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` and compare the outgoing PR title
and description with its rules. In the readable summary, identify each
broken rule and the title or description text that breaks it. Treat
this as feedback only: voice changes the verdict only if a rubric check
explicitly makes it verdict-bearing. In eval mode, ignore
`voice-guide.md` entirely.

## Component reads

Before grading, read and execute `procedure.md` as written.
`rubric.md` defines the checks, their evidence, pass conditions,
weights, and the verdict rule. Use
`references/evidence-guide.md` to locate and interpret the evidence
families named by those checks. Do not add, omit, rename, reorder, or
reinterpret rubric checks or invent a verdict rule. If the procedure
does not specify a needed step, report that procedure gap and do not
improvise a replacement. If `rubric.md` or `procedure.md` contains no
grader-written content (instruction comments do not count), refuse to
grade and explain which component is empty.

## Verdict and output

Use only the binary verdicts: `accept` means ready to submit; `reject`
means hold. Apply the rubric's verdict rule to the grades exactly as
written. End every graded reply with one valid fenced JSON block using
the schema below, with no text after it. Set `item` to the PR URL in
live mode or the bundle id in eval mode. Include one `checks` entry
for every rubric check, in rubric order, using its exact name and a
grade of `pass`, `fail`, or `unclear`. Give each entry a one-line
evidence statement identifying the fact or quote that determined its
grade. Set `verdict` to the rubric-derived `accept` or `reject`.
Readable per-check explanations may precede the JSON, but do not alter
the schema, add fields, or put anything after the block.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

For every check, cite the specific fact or quote that decided it; never
grade from impression alone. Judge the change and its evidence against
the plan, issue, and stated standards, not the polish or length of the
write-up. Apply the rubric's conditions even when a result feels
counterintuitive; revise neither criteria nor verdict ad hoc during a
run. Follow the procedure for how and where to gather evidence. Treat
`unclear` as the rubric's verdict rule directs; if that rule is silent,
an unverifiable claim fails and cannot support readiness. A disclosed
shortfall is not automatically a failure: apply the rubric's stated
conditions to the actual scope and disclosures.
