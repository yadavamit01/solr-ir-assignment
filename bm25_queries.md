# Task 4 — BM25 Ranking

## Verifying BM25 is the active similarity

1. Open `http://localhost:8983/solr/#/ir_assignment/schema` and check the
   field type `text_general` — no custom `<similarity>` means Solr's
   default `solr.BM25SimilarityFactory` is active.
2. Or run any query with `&debugQuery=true` — the `explain` block in the
   response will show terms like `weight(...) [SchemaSimilarity], result of:`
   followed by `idf`, `tf`, and `avgdl` components, which are the BM25
   formula's inputs. **Screenshot this `explain` block** as your BM25 proof.

## 5 required search queries (Top-10 each)

Run each with debug scoring:
```
http://localhost:8983/solr/ir_assignment/select?q=body:<TERM>&rows=10&fl=id,title,score&debugQuery=true
```

| # | Query (`q=`)                         | Purpose                                              |
|---|---------------------------------------|-------------------------------------------------------|
| 1 | `body:python`                        | High-frequency term across 10 docs — tests basic BM25 ranking by term frequency |
| 2 | `body:cloud`                         | Medium-frequency term across 7 docs |
| 3 | `body:security`                      | Cross-category term (Cybersecurity + Mobile + Cloud docs) — tests IDF effect |
| 4 | `title:machine learning`             | Multi-term query — tests BM25 score summation across terms |
| 5 | `body:python AND body:programming`   | Boolean + ranking combined — tests BM25 on a filtered result set |

## Reporting template (fill after running each query)

For **each** query, report a table like this using your actual scores:

| Rank | Doc ID  | Title                          | BM25 Score |
|------|---------|----------------------------------|-----------|
| 1    | doc00X  | ...                                | 2.87      |
| 2    | doc00Y  | ...                                | 2.41      |
| ...  | ...     | ...                                | ...       |

**Analysis to include per query (1–2 sentences):**
- Which document ranked #1 and why (term frequency / field length / IDF).
- Whether the ranking order matches intuitive relevance.

## Notes on BM25 in Solr
- Default parameters: `k1 = 1.2` (term-frequency saturation), `b = 0.75`
  (length normalization).
- Since our documents are short and similar in length (2–3 sentences),
  expect BM25 scores to be driven mostly by term frequency (tf) and
  inverse document frequency (idf), with length normalization playing a
  smaller role than it would on a corpus of long articles.
