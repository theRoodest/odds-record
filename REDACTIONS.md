# Files changed after their hash was published

The rule of this record is that a report file is never edited after its morning hash is committed here. When that
rule has to be broken, the change is listed below with both hashes, so that `shasum -c` failing on the file is
explained rather than hidden. Only credential leaks qualify; a pick is never edited.

| Date | File | Published hash (morning) | Hash after edit | What changed |
|---|---|---|---|---|
| 2026-10-24 | `reports/nhl-2026-10-24.md` | `2a6d859b296e660f509f332c8e48203c466acaec179e6568b9cd7002c3341180` | `6e5c167a6fc67844a1d92d4b8673b4bfa230ab3fa2668f8c92ded4c0ca12058f` | Line 242, an error message from a price source, quoted the request URL including the source's API key. The key was replaced by `REDACTED` on 2026-10-26 and the credential is being rotated by the owner. No pick, price, line or grade was touched. |
