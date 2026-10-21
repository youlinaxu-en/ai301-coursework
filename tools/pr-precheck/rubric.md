# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Files in scope | The plan's stated scope and deviation notes compared to the candidate PR's changed files and diff; the evidence lives in the plan-context block and the unified diff. | Pass only when every changed file is inside the plan's stated boundary or an explicit deviation note, and there are no silent additions, removals, or unrelated edits hidden in the branch. | required |
| Claims match diff | The PR description and title compared to the actual diff and issue; the evidence lives in the description, issue context, and the code changes. | Pass only when the description makes no claim the diff does not support, and any scope or behavior claims are consistent with the actual change. A stale, broader, or narrower summary is a fail. | required |
| Test evidence is real | The plan's test plan and the PR's test-evidence section or captured command output compared to the repo's actual validation; evidence lives in the test-evidence block and the relevant repo checks. | Pass only when the PR shows observable before/after behavior or concrete repo checks, and the evidence is tied to the plan's expected outcome. "Tests pass" with no proof, or tests not run for the changed behavior, is a fail; an unverified claim is unclear and treated as fail. | required |
| Diff is reviewable | The unified diff and commit list read for unrelated hunks, dead code, debug leftovers, commented-out code, formatting churn, or exploratory edits. | Pass only when the fix is visible and reviewable: no unrelated files, no stray debug or cleanup churn, and the commit/diff does not bury the actual change in noise. | required |
| Standards and disclosure are met | The repo-facts block's PR template, stated policy, and disclosure asks compared to the PR's title, description, and issue/maintainer thread; evidence lives in the template and the submitted text. | Pass only when the required template sections are filled with real content, any required disclosure is present, and maintainer-facing instructions are acknowledged or followed. Boilerplate or ignored asks fail this check. | required |
| Evidence quality is helpful (preferred) | The title, description, and test output read together for clarity and traceability; evidence lives in the PR text and validation notes. | Pass when the package makes the change and its proof easy to verify without guessing; this never changes the verdict by itself. | preferred |

## Verdict rule

Accept only if every required check passes. Preferred checks never change the verdict on their own. If any required check fails, the package is `reject`. If a required check is `unclear`, treat it as a fail for verdict purposes. In other words: `accept` requires all required checks to be `pass`; any `fail` or `unclear` among required checks yields `reject`.

This rubric covers the four failure families the practice submissions use: silent drift (Files in scope and Claims match diff), not tested (Test evidence is real), unreviewable (Diff is reviewable), and standards wall (Standards and disclosure are met).
