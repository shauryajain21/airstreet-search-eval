# Air Street search eval: Linkup re-run

Air Street Capital compared Linkup, Exa, Parallel and Tavily on two benchmarks on 2026-09-29. We re-ran Linkup on the same questions, with the same answer, judge and review prompts, in two new configurations:

- **Linkup optimized:** `depth: standard`, queries written following [Linkup's query guidance](https://github.com/LinkupPlatform/linkup-for-agents), and Linkup's default number of results.
- **Linkup deep optimized:** optimized queries, `depth: deep`.

The optimized queries are in [`queries/`](queries). They apply one fixed template per benchmark ([`prompts/optimized-query-templates.json`](prompts/optimized-query-templates.json)) and add no answers or source URLs.

## Factual QA

28 questions, 3 trials each. A trial passes when the answer is complete, correct and supported by the retrieved evidence.

| Configuration | Supported answers | Pass rate |
|---|---:|---:|
| Exa auto | 81/84 | 96.4% |
| **Linkup optimized** | **77/84** | **91.7%** |
| Parallel basic | 76/84 | 90.5% |
| Linkup (as originally tested) | 69/84 | 82.1% |
| Tavily basic | 63/84 | 75.0% |

## Harder retrieval

16 research questions, each with 3 evidence criteria scored 0, 0.5 or 1. The evidence is two searches plus the fetched text of one selected URL per search. A question is complete when all three criteria score 1.

| Configuration | Complete evidence | Evidence points |
|---|---:|---:|
| **Linkup deep optimized** | **13/16** | **46.25/48** |
| Exa auto + Contents | 12/16 | 45.5/48 |
| **Linkup optimized** | **10/16** | **43/48** |
| Parallel basic + Extract | 8/16 | 43/48 |
| Tavily basic + basic Extract | 8/16 | 41.5/48 |
| Linkup (as originally tested) | 7/16 | 39/48 |

Non-bold rows are the scores published by the original evaluation. Bold rows were graded with the original prompts, using OpenAI models in place of the original graders, then placed on the original scale. That shift equals the gap between our score for Linkup as originally tested and its published score.

Every request, returned URL, answer and grade behind the tables is in [`results/`](results).
