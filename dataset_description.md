# Dataset Description

**File:** `documents.json`
**Number of documents:** 55
**Domain:** Technology news / short articles

## Fields (schema)

| Field      | Type                | Description                                             |
|------------|---------------------|----------------------------------------------------------|
| `id`       | string (unique key) | Unique document identifier, e.g. `doc001`                |
| `title`    | text_general        | Short headline of the article                            |
| `body`     | text_general        | 2–3 sentence article body — main searchable content       |
| `category` | string (facet-able) | Topic category, e.g. Programming, Cloud, Cybersecurity    |
| `author`   | string              | Author name                                               |
| `tags`     | string (multi-valued)| Keyword tags associated with the article                 |

## Topic coverage (why these topics were chosen)

The 55 documents were written (not scraped) so that term frequencies are
controllable and every required query type produces an explainable result:

- **Python** — 10 docs (varying density of "python" and "programming")
- **Java** — 7 docs
- **Machine Learning / Deep Learning** — 8 docs
- **Cloud Computing** — 7 docs
- **Web Development** — 6 docs
- **Databases** — 5 docs
- **Cybersecurity** — 5 docs
- **Mobile Development** — 4 docs
- **Blockchain / DevOps** — 3 docs

This overlap is intentional: e.g. "python" and "java" both appear in doc007,
"machine learning" appears in both the Machine Learning and Finance/Healthcare
categories, and "mobile" + "security" overlap in doc051. This lets the
Boolean AND / OR / AND NOT / nested queries return different, meaningful
result sets instead of trivial all-or-nothing matches.

## Source / originality

Documents are original short-form summaries written for this assignment
(not copied from any website), so there are no copyright/licensing concerns
when submitting the dataset.
