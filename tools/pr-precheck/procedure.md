# Procedure: how this tool grades a PR package

## Read order

1. In live mode, read `scope.md` first. Stop without grading if its
   `Repo:` line is an unfilled placeholder; refuse if the candidate is
   for a repository outside that scope. Record the scoped repository
   and its house rules. In eval mode, do not read `scope.md`.
2. Read `rubric.md`, `references/evidence-guide.md`, and this procedure
   before inspecting the package. If either the rubric or procedure
   has no grader-written content, refuse to grade. Use the rubric's
   check names, order, weights, pass conditions, and verdict rule
   without adding criteria.
3. Read the plan context before the candidate PR. In live mode, read
   `plan.md` and its deviation notes, or the house plan and house
   reproduction pack for a house-chain submission; identify the linked
   issue and read its thread in the scoped repository. In eval mode,
   read the bundle's plan-context and issue-context sections. Record
   the promised scope/boundary, expected behavior, test plan, and any
   explicit deviations or disclosed shortfalls. These are the
   baselines for the comparisons below.
4. Read repository standards before judging compliance. In live mode,
   inspect the scoped repository's PR template, contributing
   instructions, and applicable stated policy, including AI-use
   disclosure and maintainer directions in the issue thread. In eval
   mode, read the repo-facts block for these asks. Record each
   applicable requirement. Do not infer an unstated requirement.
5. Read the candidate package: title and description, commit list,
   complete diff, and test evidence. In live mode, obtain the complete
   branch diff from the working copy using
   `git diff <default-branch>...HEAD` (three dots; use `main` when it
   is the repository's default branch). In eval mode, use only the
   corresponding bundle sections. Read the description after the
   plan and diff so its claims can be checked against both.
6. In live mode, read `voice-guide.md` and compare its rules with the
   draft title and description. Report broken voice rules in the
   readable summary; do not make them verdict-bearing unless a rubric
   check explicitly does so. Ignore the voice guide in eval mode.

## Evidence gathering

Build a concise evidence ledger before assigning grades. For each
gather, record the source and the specific fact, quote, file, or
observable result; keep the plan and candidate evidence side by side.

- **Plan fidelity / Files in scope:** List the files and behavioral
  changes named by the plan's scope and boundary, plus those permitted
  by explicit deviation notes. List the files and behavior actually
  changed in the unified diff. Compare both lists in both directions:
  identify actual changes not authorized by the plan and planned
  changes absent from the diff. Treat an explicit deviation or
  disclosed shortfall as disclosed, not silent drift; retain the exact
  note and assess it under the rubric's pass condition.
- **Description claims / Claims match diff:** Extract each material
  claim in the title and description about the issue, scope, behavior,
  files, tests, and outcome. For each claim, record the supporting or
  contradicting diff hunk, plan detail, or test result. Do not treat
  the description's own assertion as proof that the diff delivers it.
- **Test evidence:** Put each planned test or expected behavior next
  to the submitted evidence for it. Record the command or reproduction
  step, the observable before/after or expected result, and its actual
  output/status. Separately record the relevant repository checks or
  suite and whether they were run and passed. In eval mode use the
  bundle's test-evidence block; in live mode use captured output and
  the repository's checks. A bare assertion such as "tests pass" is
  not an observable result.
- **Diff quality:** Review the unified diff and commit list for the
  fix itself, unrelated files or hunks, debug leftovers, dead code,
  commented-out blocks, formatting churn, and drive-by edits. Record
  the exact files or hunks that help or hinder review; do not infer
  noise solely from commit count or diff size.
- **Standards and disclosure:** Make a checklist of the applicable
  template sections, policy/disclosure requirements, and explicit
  maintainer directions. Compare each item to the title/description
  and issue-thread response; record where real content satisfies it
  or where it is blank, boilerplate, omitted, or ignored.
- **Files and Claims tables, when present in the package:** Inspect
  every row. Map each `no` in Files to the scope/deviation comparison
  and each `no` in Claims to the description-versus-diff comparison.
  Record the row and its evidence; do not overlook a `no` because
  another part of the package describes the result positively.
- **Preferred evidence-quality check:** Use the gathered title,
  description, and test results to record whether a reviewer can trace
  the change and proof without guessing. This check is not a substitute
  for any required check.

Use the locations in `references/evidence-guide.md` for the relevant
mode. If a source is missing, record it as absent rather than filling
the gap with assumptions.

## Check execution

Execute every rubric check in the rubric's listed order, using only the
evidence ledger and the check's stated pass condition:

1. Grade **Files in scope** from the two-way comparison of planned and
   actual changes, including the plan's explicit deviation notes.
2. Grade **Claims match diff** by matching each material title and
   description claim to the plan and actual diff; a contradiction or
   unsupported claim is not cured by accurate claims elsewhere.
3. Grade **Test evidence is real** by comparing planned expected
   behavior to observable evidence and checking the outcome of the
   repository's applicable validation.
4. Grade **Diff is reviewable** from the actual diff and commit content,
   citing concrete unrelated or obstructive material when present.
5. Grade **Standards and disclosure are met** against each applicable
   template, policy, disclosure, and maintainer ask recorded earlier.
6. Grade any preferred checks using their own rubric conditions.

Assign `pass` only when the pass condition is affirmatively supported
by recorded evidence. Assign `fail` when evidence demonstrates that a
pass condition is not met, including any `no` row mapped to a check.
Assign `unclear` when evidence needed to decide is genuinely absent or
unverifiable; do not turn absence into a positive claim. An explicitly
disclosed shortfall is not automatically a failure: apply the exact
rubric condition to the disclosure and the actual delivered scope.
Each check may be graded from its corresponding ledger entries; do not
reopen unrelated package evidence or add an unlisted criterion.

## Verdict assembly

Apply the verdict rule in `rubric.md` without modification: `accept`
only when every required check is `pass`; any required `fail` or
`unclear` produces `reject`. Preferred checks never change the
verdict. If the verdict is `reject`, identify as the deciding check
the first required check in rubric order graded `fail` or `unclear`.
In the readable summary, explain that check with its strongest
recorded fact or quote; if additional required checks also failed,
list them there as well.

Return one result for this package only. Include every rubric check,
in rubric order, with its exact name, grade, and a one-line evidence
statement naming the decisive fact or quote. Use the PR URL as `item`
in live mode and the bundle id in eval mode. End with the exact fenced
JSON schema required by `SKILL.md`; ensure the JSON is valid and that
nothing follows the closing fence.
