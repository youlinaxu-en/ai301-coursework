# DRAFT for beat-1-sandbox/unit-1/selection.md

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68

**Verdict output**

All four candidates accept — every required check passes on each.
Ranked by fit profile:

1. #68 — Keyword search raises ZeroDivisionError when the index is
   empty (rag, tier-1, good first issue). Best fit: retriever code like
   my own coursework project; defensive error handling plus a
   test-driven finish (drop the strict xfail marker). One classmate
   claim comment (2026-09-19); the Path Review house rule says that
   does not block.
2. #72 — verify_password raises UnknownHashError instead of returning
   False (api, tier-1). Fail-closed error handling in core/security.py
   with the same xfail workflow; one classmate claim (2026-09-22).
3. #53 — PII scrubber misses parenthesized US phone numbers (safety,
   tier-1). Regex practice; a classmate has already posted a full
   reproduction report in-thread (does not block, but the ground is
   more shared).
4. #73 — README and .env.example disagree about the LLM API key (docs,
   tier-1). Completely unclaimed and the fastest win, but a docs/config
   alignment gives the least backend practice.

Preferred checks graded identically on all four (maintainer-endorsed
and no-abandoned-attempts pass; release-recent and maintainer-responsive
fail — the repo has no releases and no maintainer first-responses in
the 5-issue sample), so the fit profile decided the ranking.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "archived: false; last push 2026-09-16, 6 days before grading date 2026-09-22"},
      {"name": "maintainer-active", "grade": "pass", "evidence": "all 5 latest default-branch commits are human-authored by Aburke225, 2026-08-24 to 2026-09-16"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "maintainer-filed single fix: guard empty corpus in KeywordSearcher.index() to mirror search(), named files, drop xfail H-01, est. 2-4h"},
      {"name": "unclaimed", "grade": "pass", "evidence": "no assignee, no open or linked PRs; one student claim comment (acordero4852, 2026-09-19) ignored per Path Review house rule"},
      {"name": "policy-allows-ai", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template state workflow conditions only; no AI policy stated anywhere — silence passes"},
      {"name": "release-recent", "grade": "fail", "evidence": "no releases published"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "0 of 5 recently commented issues (#72,#69,#68,#62,#60) have any maintainer first response"},
      {"name": "maintainer-endorsed", "grade": "pass", "evidence": "good first issue label; opened by Aburke225 (COLLABORATOR)"},
      {"name": "no-abandoned-attempts", "grade": "pass", "evidence": "timeline shows no linked PRs, open or closed"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "archived: false; last push 2026-09-16, 6 days before grading date 2026-09-22"},
      {"name": "maintainer-active", "grade": "pass", "evidence": "all 5 latest default-branch commits are human-authored by Aburke225, 2026-08-24 to 2026-09-16"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "maintainer-filed single fix: make verify_password fail closed on UnknownHashError in core/security.py, drop xfail H-05, est. 1-2h"},
      {"name": "unclaimed", "grade": "pass", "evidence": "no assignee, no open PRs; one student claim comment (sseid4, 2026-09-22) ignored per Path Review house rule"},
      {"name": "policy-allows-ai", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template state workflow conditions only; no AI policy stated anywhere — silence passes"},
      {"name": "release-recent", "grade": "fail", "evidence": "no releases published"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "0 of 5 recently commented issues (#72,#69,#68,#62,#60) have any maintainer first response"},
      {"name": "maintainer-endorsed", "grade": "pass", "evidence": "good first issue label; opened by Aburke225 (COLLABORATOR)"},
      {"name": "no-abandoned-attempts", "grade": "pass", "evidence": "timeline shows commit references only, no PRs open or closed"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/53",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "archived: false; last push 2026-09-16, 6 days before grading date 2026-09-22"},
      {"name": "maintainer-active", "grade": "pass", "evidence": "all 5 latest default-branch commits are human-authored by Aburke225, 2026-08-24 to 2026-09-16"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "maintainer-filed single regex fix in safety/pii_scrubber.py with repro snippet and 4 named failing tests"},
      {"name": "unclaimed", "grade": "pass", "evidence": "no assignee, no open or linked PRs; one student's claim plus repro report (bhargavchintam, 2026-09-22) ignored per Path Review house rule"},
      {"name": "policy-allows-ai", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template state workflow conditions only; no AI policy stated anywhere — silence passes"},
      {"name": "release-recent", "grade": "fail", "evidence": "no releases published"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "0 of 5 recently commented issues (#72,#69,#68,#62,#60) have any maintainer first response"},
      {"name": "maintainer-endorsed", "grade": "pass", "evidence": "good first issue label; opened by Aburke225 (COLLABORATOR)"},
      {"name": "no-abandoned-attempts", "grade": "pass", "evidence": "timeline shows no linked PRs, open or closed"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73",
    "checks": [
      {"name": "repo-alive", "grade": "pass", "evidence": "archived: false; last push 2026-09-16, 6 days before grading date 2026-09-22"},
      {"name": "maintainer-active", "grade": "pass", "evidence": "all 5 latest default-branch commits are human-authored by Aburke225, 2026-08-24 to 2026-09-16"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "maintainer-filed single docs/config alignment between README.md and .env.example, est. 1-2h"},
      {"name": "unclaimed", "grade": "pass", "evidence": "no assignee, no linked PRs, zero comments on the thread"},
      {"name": "policy-allows-ai", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template state workflow conditions only; no AI policy stated anywhere — silence passes"},
      {"name": "release-recent", "grade": "fail", "evidence": "no releases published"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "0 of 5 recently commented issues (#72,#69,#68,#62,#60) have any maintainer first response"},
      {"name": "maintainer-endorsed", "grade": "pass", "evidence": "good first issue label; opened by Aburke225 (COLLABORATOR)"},
      {"name": "no-abandoned-attempts", "grade": "pass", "evidence": "no linked PRs, open or closed"}
    ],
    "verdict": "accept"
  }
]
```

## Eval iterations

**Run history**

One full run: 18/20. The confirming run's closing line in eval-run.txt,
"agreement: 18/20 scored items  (bar: 18/20: PASS)". 

**Issue analysis**

issue-19. My rubric: reject (failed scope-bounded). Gold label: accept
("maintainer-diagnosed performance bug with named causes, unclaimed").
The bundle's issue is a zxlive performance bug whose maintainer-opener
diagnoses it in the issue body (the comment thread is empty): "There are
two potential causes which should be fixed: 1. The matchers are slow
for certain rewrites (quadratic instead of linear) 2. UI update is
waiting for the matching thread to finish", followed by three
"Additional suggestions" such as multi-processing. My scope-bounded
check requires "exactly one bounded change with a settled spec: what to
change is stated by the opener or confirmed by a maintainer in the
thread." The grader read two named causes plus three optional
suggestions as more than one bounded change with an unsettled "what",
and failed the check, where the gold label reads the same diagnosis as
the settled spec itself. The reject came from my check treating a
multi-cause diagnosis as an open design question rather than a scoped
work list.

**Check rationale**

From my rubric.md, the scope-bounded pass condition,  "The issue
asks for exactly one bounded change with a settled spec: what to change
is stated by the opener or confirmed by a maintainer in the thread. A
terse body, a checklist of acceptance criteria, or a bug report without
repro steps still passes when the work asked for is one bounded change.
Fails on any scope trigger listed below the table." It is written this
way because the scope family kills first contributions in two opposite
ways: umbrella issues and design debates are too big, while terse
maintainer-filed bugs only look too small. The explicit
terse-but-bounded sentence exists so the check does not punish short
write-ups, and the five fail triggers name the actual killers (tracking
lists, unsettled debates, core-internals warnings, support questions,
spec-less wishes) instead of leaving "bounded" to taste.

**Trade-offs**

The quoted check changes the result on issue-19: gold accepts it, my
rubric rejects it, because the check reads a maintainer's multi-cause
performance diagnosis as an unsettled spec. It also leans the other way
on issue-15, which gold rejects as "years of design debate and two
abandoned PRs behind a friendly label" (gold-labels.json) but my rubric
accepts. I kept the wording anyway: the run stands at 18/20 with every category matched,
and rephrasing the check to flip exactly those two bundles would be
tuning to the test set rather than to the judgment the check encodes.

## Selection rationale


1. Fit and time: #68 is a Python backend bug in a retriever module, the same kind of code as my coursework RAG project, and the maintainer estimates 2–4 hours, which fits the unit's window.
2. What the verdict identified correctly, and what I weighed beyond it: the checks correctly established the repo is alive, the scope is one settled change with a covering xfail test, and the policy is silent on AI use. Beyond the rubric, I weighed two things it cannot see: a classmate had already claimed #68 in the thread, which the house rule says does not block, and the fix is small enough that parallel work costs neither of us anything; and the failed maintainer-responsive check reads worse than reality, because this is a seeded classroom tracker where staff review pull requests rather than reply in issue threads.
3. Anticipated difficulty in claiming: low — claiming is a comment, and the house rule makes shared claims normal. The real friction I expect is mechanical: my first fork PR will sit at "waiting for approval to run workflows" until a maintainer releases CI, and the fix must also remove the strict xfail marker, or CI fails on XPASS(strict).
