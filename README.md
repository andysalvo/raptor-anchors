# raptor-anchors

Daily Merkle-root anchors for the Raptor Intelligence event ledger.

Every night, Raptor computes a Merkle root over the chain heads of all of its
hash-chained source streams and commits it here. Because this repo is public and
GitHub timestamps every commit, each anchor is third-party proof that the ledger's
history existed — unaltered — as of that date.

Format: `anchors/YYYY-MM-DD.json` → `{ "date", "merkle_root", "source_heads": { ... } }`

Verify any Raptor fact permalink against these anchors: the fact's chain hash must
be reachable from the anchored root for its capture date.
