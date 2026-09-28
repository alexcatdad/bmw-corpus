# bmw-corpus
Public BMW source corpus with captured artifacts, provenance, and normalized outputs, beginning with E30 and E46.

Captured input stays immutable in `raw/sha256/`; `captures/` records origin,
redistribution approval, retrieval metadata, hash, and fixture status. Captures
are source evidence, not independently verified automotive facts.

The prepared normalization workflow calls a pinned version of
[bmw-knowledge](https://github.com/alexcatdad/bmw-knowledge). Small derived files
live in `normalized/<capture-id>/<processor-revision>/`; `processing/` receipts
record input/output hashes, processor version, and known losses. The same CLI
runs locally. Application code and operational research/job state live in the
software repository and Convex.

Follow [RUNBOOK.md](RUNBOOK.md) before enabling the workflow. It requires a
dedicated processing callback secret and URL. No live captured or normalized
source has been published yet. Project-owned test fixtures must remain labelled
and must not be counted as BMW evidence.
