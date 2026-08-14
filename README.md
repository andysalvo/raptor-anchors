# raptor-anchors

Daily Merkle-root anchors for the Raptor Intelligence event ledger.

Every night, Raptor computes a Merkle root over the chain heads of all of its
hash-chained source streams and commits it here. Because this repo is public and
GitHub timestamps every commit, each anchor is third-party proof that the ledger's
history existed — unaltered — as of that date.

Format: `anchors/YYYY-MM-DD.json` → `{ "date", "merkle_root", "source_heads": { ... } }`

Verify any Raptor fact permalink against these anchors: the fact's chain hash must
be reachable from the anchored root for its capture date.

---

## Where development ended and production began (2026-08-13)

The anchors dated **2026-08-12** and **2026-08-13** commit to Merkle roots over a
ledger that was still under development. Nothing in it was ever public, and no
customer ever read from it. On 2026-08-13 it was retired: a re-runnable gate
script had been committing synthetic test fixtures — including fabricated
acquisition events — into the chain on every run, and a ledger whose product is
a verifiable record cannot carry fabricated records, filterable or not.

That development ledger was **archived, not deleted.** It is preserved intact,
append-only triggers and all, in a `lake_dev_archive` schema, so the two anchors
above remain checkable against exactly the data they committed to. Deleting it
would have left two public commitments whose subject no longer existed.

One stream crossed the line unchanged. The `pricing` stream's 27 documents were
re-laid into the new ledger from a hash-verified export, in the same order, from
the same genesis of 32 zero bytes. Because the canonical envelope covers only
(source_id, external_id, fetched_at, content_sha256), every link reproduced its
original hash exactly, and the stream's head is bit-for-bit identical:

    pricing  fea2f7582feeabbb354d9ef17d40b99820d9024049dd3ee29632a04ba1189d17

So the `pricing` head published in the 2026-08-13 anchor still verifies against
the production ledger. The other streams from the development period
(`hn`, `github`, `yc`, `mcp_registry`, `edgar_formd`, `test:gate`) end there and
do not continue; anchors from **2026-08-14** onward cover the production ledger,
which begins from genesis.

Merkle roots before and after that date are therefore **not** expected to relate
to each other. This section is the explanation of that discontinuity, and it is
the last one there will be: the gate no longer writes to the chain at all.
