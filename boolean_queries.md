# Task 3 — Boolean Queries

All queries below target the `body` field (works the same on `title`).
Run via Admin UI query tab, or curl:

```
curl "http://localhost:8983/solr/ir_assignment/select?q=<QUERY>"
```

## I. Term1 AND Term2

**Query:** `body:python AND body:machine`
```
q=body:python AND body:machine
```
**Expect:** doc004 ("Machine Learning with Python") — the only document
containing both "python" and "machine".

## II. Term1 OR Term2

**Query:** `body:python OR body:java`
```
q=body:python OR body:java
```
**Expect:** union of all Python docs (doc001–doc010) and all Java docs
(doc011–doc017), including doc007 which mentions both — 17 total matches.

## III. Term1 AND NOT Term2

**Query:** `body:python AND NOT body:java`
```
q=body:python AND NOT body:java
```
**Expect:** all Python docs EXCEPT doc007 ("Python vs Java Performance"),
i.e. 9 documents.

## IV. Nested Boolean Query

**Query:** `(body:python OR body:java) AND (body:web OR body:cloud) AND NOT body:mobile`
```
q=(body:python OR body:java) AND (body:web OR body:cloud) AND NOT body:mobile
```
**Expect:** doc003 ("Python Web Frameworks") and doc013 ("Spring Framework
for Java") — documents about Python/Java that also mention web or cloud,
excluding anything about mobile development.

---

### What to screenshot for the report
For each of the 4 queries: the Admin UI "Query" tab with the `q=` box
filled in, the response `numFound`, and the returned `id`/`title` fields.
