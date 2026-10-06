# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

youlinaxu-en

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68#issuecomment-6009071925
## Plan for Issue #68

I reproduced Issue #68 and confirmed that `KeywordSearcher.index([])`
passes an empty tokenized corpus to `BM25Okapi`, which causes
`rank-bm25` to divide by a corpus size of zero and raise a
`ZeroDivisionError`.

### Diagnosis

The Unit 2 reproduction showed the failure path:

```text
KeywordSearcher.index([])
→ tokenized_corpus = []
→ BM25Okapi([])
→ corpus_size = 0
→ ZeroDivisionError

Scope
I plan to:
- update KeywordSearcher.index() so an empty chunks list is handled
  before BM25Okapi is initialized;
- preserve the empty chunk list as the current index state;
- update the existing empty-index test so it verifies expected behavior
  instead of relying on xfail;
- verify that non-empty keyword-search behavior remains unchanged.
The existing search() implementation already handles an empty index by
returning [] when self.bm25 or self.chunks is empty, so I do not
plan to modify the search path.
I do not plan to change:
- the rank-bm25 dependency;
- BM25 scoring or ranking behavior;
- tokenization behavior;
- unrelated retriever components.
Files
Expected files to change:
- rag/retriever/keyword_search.py
- tests/unit/test_keyword_search.py
Approach
In KeywordSearcher.index(), I will detect the empty-corpus case before
constructing BM25Okapi.
For an empty corpus, the method will preserve the empty chunk list,
leave the BM25 index in an empty state such as None, and return before
calling BM25Okapi([]).
For non-empty corpora, the existing tokenization and BM25 initialization
path will remain unchanged.
The implementation branch will follow the repository convention:
fix/68-empty-bm25-index
Test Plan
I will re-run the Unit 2 reproduction command:
python -m pytest .\tests\unit\test_keyword_search.py -v --runxfail --tb=long

Before the fix, the empty-index test raises:
ZeroDivisionError: division by zero

After the fix:
- KeywordSearcher.index([]) should complete without raising;
- searching the empty index should return [];
- the empty-index test should pass without relying on xfail.
I will then run:
python -m pytest .\tests\unit\test_keyword_search.py -v

The complete keyword-search unit test file should pass, including the
existing non-empty search cases.
---

## Your branch

**Branch**
fix/68-empty-bm25-index

**Evidence**

Before
The Unit 2 reproduction used:
python -m pytest .\tests\unit\test_keyword_search.py -v --runxfail --tb=long

The relevant failure output was:
TestKeywordSearcher.test_empty_index

>       searcher.index([])
tests\unit\test_keyword_search.py:140

>       self.bm25 = BM25Okapi(tokenized_corpus)
rag\retriever\keyword_search.py:25

>       self.avgdl = num_doc / self.corpus_size
E       ZeroDivisionError: division by zero
.venv\Lib\site-packages\rank_bm25.py:52: ZeroDivisionError

The reproduction showed that KeywordSearcher.index([]) passed an empty
tokenized corpus to BM25Okapi, causing rank-bm25 to divide by a corpus
size of zero.
After
I re-ran the Unit 2 reproduction command against the implemented fix:
py -m pytest .\tests\unit\test_keyword_search.py -v --runxfail --tb=long

Output:
========================================================= test session starts ==========================================================
platform win32 -- Python 3.14.5, pytest-9.1.1, pluggy-1.6.0 -- C:\Users\www33\Desktop\Class\pathreview-ai301-fa26-s3\.venv\Scripts\python.exe
cachedir: .pytest_cache
rootdir: C:\Users\www33\Desktop\Class\pathreview-ai301-fa26-s3
configfile: pyproject.toml
plugins: anyio-4.15.1
collected 17 items

tests/unit/test_keyword_search.py::TestKeywordSearcher::test_results_sorted_by_score_descending PASSED                            [  5%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_query_matching_no_documents PASSED                                   [ 11%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_query_matching_multiple_documents PASSED                             [ 17%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_case_insensitive_matching PASSED                                     [ 23%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_top_k_limit PASSED                                                   [ 29%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_top_k_larger_than_results PASSED                                     [ 35%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_results_have_bm25_score PASSED                                       [ 41%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_results_preserve_chunk_fields PASSED                                 [ 47%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index PASSED                                                   [ 52%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_index_not_called_returns_empty PASSED                                [ 58%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_multi_word_query PASSED                                              [ 64%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_tokenization PASSED                                                  [ 70%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_tokenization_case_handling PASSED                                    [ 76%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_large_corpus PASSED                                                  [ 82%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_special_characters_in_query PASSED                                   [ 88%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_exact_phrase_matching PASSED                                         [ 94%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_single_word_chunks PASSED                                            [100%]

========================================================== 17 passed in 0.94s ==========================================================

I also ran the complete keyword-search unit test file normally:
python -m pytest .\tests\unit\test_keyword_search.py -v

Output:
========================================================= test session starts ==========================================================
platform win32 -- Python 3.14.5, pytest-9.1.1, pluggy-1.6.0 -- C:\Users\www33\Desktop\Class\pathreview-ai301-fa26-s3\.venv\Scripts\python.exe
cachedir: .pytest_cache
rootdir: C:\Users\www33\Desktop\Class\pathreview-ai301-fa26-s3
configfile: pyproject.toml
plugins: anyio-4.15.1
collected 17 items

tests/unit/test_keyword_search.py::TestKeywordSearcher::test_results_sorted_by_score_descending PASSED                            [  5%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_query_matching_no_documents PASSED                                   [ 11%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_query_matching_multiple_documents PASSED                             [ 17%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_case_insensitive_matching PASSED                                     [ 23%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_top_k_limit PASSED                                                   [ 29%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_top_k_larger_than_results PASSED                                     [ 35%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_results_have_bm25_score PASSED                                       [ 41%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_results_preserve_chunk_fields PASSED                                 [ 47%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index PASSED                                                   [ 52%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_index_not_called_returns_empty PASSED                                [ 58%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_multi_word_query PASSED                                              [ 64%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_tokenization PASSED                                                  [ 70%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_tokenization_case_handling PASSED                                    [ 76%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_large_corpus PASSED                                                  [ 82%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_special_characters_in_query PASSED                                   [ 88%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_exact_phrase_matching PASSED                                         [ 94%]
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_single_word_chunks PASSED                                            [100%]

========================================================== 17 passed in 0.30s ==========================================================

The previously failing test_empty_index now passes, and all 17 tests in
tests/unit/test_keyword_search.py pass. This verifies both the empty-index
fix and preservation of existing non-empty keyword-search behavior.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Run history
grading 20 package(s) with rubric.md + evidence-guide.md + procedure.md, model sonnet, 5 worker(s)...
  pkg-01: reject
  pkg-03: accept
  pkg-02: accept
  pkg-05: reject
  pkg-04: reject
  pkg-07: reject
  pkg-06: reject
  pkg-10: reject
  pkg-08: accept
  pkg-09: accept
  pkg-13: accept
  pkg-12: reject
  pkg-11: reject
  pkg-15: reject
  pkg-17: reject
  pkg-14: reject
  pkg-18: reject
  pkg-16: reject
  pkg-19: reject
  pkg-20: reject

item    category           gold    verdict  agree  note
pkg-01  wrong-cause        reject  reject   yes    
pkg-02  clear-accept       accept  accept   yes    
pkg-03  clear-accept       accept  accept   yes    
pkg-04  thread-convention  reject  reject   yes    
pkg-05  clear-accept       accept  reject   NO     failed: Honesty about uncertainty
pkg-06  scope-creep        reject  reject   yes    
pkg-07  wrong-cause        reject  reject   yes    
pkg-08  clear-accept       accept  accept   yes    
pkg-09  clear-accept       accept  accept   yes    
pkg-10  unbuildable        reject  reject   yes    
pkg-11  wrong-cause        reject  reject   yes    
pkg-12  scope-creep        reject  reject   yes    
pkg-13  clear-accept       accept  accept   yes    
pkg-14  clear-accept       accept  reject   NO     failed: Executable plan for a stranger, Honesty about uncertainty
pkg-15  scope-creep        reject  reject   yes    
pkg-16  wrong-cause        reject  reject   yes    
pkg-17  unbuildable        reject  reject   yes    
pkg-18  unbuildable        reject  reject   yes    
pkg-19  scope-creep        reject  reject   yes    
pkg-20  thread-convention  reject  reject   yes 
- Full run 1: 18/20
Final run output:
categories: clear-accept 5/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4
agreement: 18/20 scored items  (bar: 18/20: PASS)

The final full run met the required agreement threshold of 18/20, and
every evaluation category had at least one matching package.

**Package analysis**

Package: pkg-05
My rubric verdict: reject
Gold label: accept
The eval output recorded:
pkg-05  clear-accept  accept  reject   NO     failed: Honesty about uncertainty

My rubric rejected this package because the Honesty about uncertainty
check did not pass. The rubric therefore treated the plan as having unresolved
or insufficiently qualified uncertainty that should block acceptance, while
the gold label treated the package as ready.
This disagreement shows that my rubric is stricter than the gold label about
how clearly a plan must distinguish confirmed facts from unresolved questions
or assumptions. For pkg-05, that strictness caused a false rejection: the
gold label considered the package a clear accept, while my rubric rejected it
because of the uncertainty check.
I kept the final rubric because the complete run still reached 18/20.
It also correctly matched every package in the scope-creep,
thread-convention, unbuildable, and wrong-cause categories. The only
disagreements were two packages in the clear-accept category.

**Check rationale**

Honesty about uncertainty

I included this check because a technically plausible implementation plan can
still be misleading if it presents an assumption as confirmed repository
behavior or leaves an important unresolved question without acknowledging it.
This became relevant while checking my own Issue #68 plan. My earlier draft
treated empty-search handling as work that still needed to be implemented.
After checking the current repository code, I confirmed that search() already
contained an empty-index guard:
if not self.bm25 or not self.chunks:    return []


I therefore revised the plan so that the existing search behavior was described
as confirmed behavior rather than planned work. The actual implementation was
then limited to preventing KeywordSearcher.index([]) from constructing
BM25Okapi([]).
I kept this check because it encourages a plan to distinguish among
evidence-backed facts, implementation decisions, and genuine remaining
unknowns instead of presenting all three with the same level of certainty.

**Trade-offs**

The Honesty about uncertainty check makes the rubric conservative about plans
that leave assumptions unresolved or describe uncertain behavior too
confidently.
The trade-off is visible in pkg-05. The gold label was accept, but my
rubric returned reject because:
failed: Honesty about uncertainty

This means the check can reject an otherwise acceptable plan when the remaining
uncertainty is minor enough that the gold label does not consider it blocking.
A similar effect appears in pkg-14, where the gold label was also accept
but my rubric returned reject because of:
failed: Executable plan for a stranger, Honesty about uncertainty

I accepted this trade-off rather than loosening the check only to recover those
two clear-accept packages. The final rubric still reached:
agreement: 18/20 scored items  (bar: 18/20: PASS)

and matched every package in the scope-creep, thread-convention,
unbuildable, and wrong-cause categories. I therefore kept the stricter
uncertainty requirement because it helps prevent unsupported assumptions from
being presented as implementation facts.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
