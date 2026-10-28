# Odds Generator — public track record

This repository is the tamper-evidence for a sports-betting value finder's daily reports. The pipeline itself
is private. The record page built from it is https://theroodest.github.io/odds-record/ (`index.html`, with the
same numbers in `record.json`). What is public here:

- `hashes/<date>.sha256`: the SHA-256 of every report written on that date, committed the same morning,
  before any of the games start. A hash proves the report existed, unchanged, when the manifest was committed.
  The manifest is append-only: a name already listed keeps its morning hash; a later run of the same sport is
  saved under a timestamped name (`<sport>-<date>_HHMM.md`) and added, never substituted.
- `source-commits.txt`: for each date, the commit in the private source repository that holds the reports.
- `reports/`: the report files themselves, released 7 days after their date, once every game in them has
  started. A file is released only if it still matches its published hash, or if `REDACTIONS.md` lists the
  change with both hashes. Anything else is held back and named in the private log.
- `REDACTIONS.md`: every edit ever made to a hashed file, with the hash before and after. Two things qualify:
  a credential quoted inside an error message, and personal data about the owner. A pick never changes.

## Verifying a released file

```
git clone https://github.com/theRoodest/odds-record && cd odds-record/reports
shasum -a 256 -c ../hashes/2026-10-20.sha256        # "OK" per file; "FAILED open or read" = not yet released
```

A file that fails with a different hash must have a row in `REDACTIONS.md` whose "hash after edit" matches it;
otherwise it should not be here at all. Then check *when* the manifest existed:

1. The commit time on GitHub (`git log --format='%ci %h' -- hashes/<date>.sha256`). Git timestamps are set by the
   committing machine, so on their own they only show consistency, not proof.
2. The Internet Archive: after each morning's push the manifest's raw URL is submitted to web.archive.org, whose
   capture time is set by their servers, not by this project. Look it up at
   `https://web.archive.org/web/*/https://raw.githubusercontent.com/theRoodest/odds-record/main/hashes/<date>.sha256`.
   Captures begin with the 2026-10-28 manifest.
3. The private source commit named in `source-commits.txt` can be shown to a reviewer under NDA; it is not public.

## What is and is not attested

- Files from before 2026-10-18 (the first manifest) and from 2026-10-19 (a run that aborted before publishing) are
  in no manifest; they are history, not evidence.
- The first manifest, `hashes/2026-10-18.sha256`, was committed at 21:41 local time on 2026-10-18, after that
  day's games had started; it attests the files only as of that evening. Every later manifest was committed
  between 06:00 and 08:05 local time.
- The twelve un-timestamped reports of 2026-10-21 (`<sport>-2026-10-21.md`) were overwritten by an evening
  re-run that day, before the pipeline protected hashed files from being rewritten. Their morning hashes stand in
  the manifest, but the current files no longer match them and they will not be released. The timestamped
  `_HHMM` files of that day are unaffected. The protection (a later run is saved beside a hashed file, never over
  it) has been in place since 2026-10-26.

## History rewrite of 2026-10-27

On 2026-10-27 the commit history was rewritten once, to replace the author's personal e-mail addresses with a
GitHub no-reply address. File contents, trees and commit times were not touched; only author/committer name
and e-mail changed, so every commit id did. The repository had no forks, stars or watchers at the time. This
will not happen again: the point of the record is that it is not rewritten. Old and new ids:

  | Before | After |
  |---|---|
  | `88a67ea` | `7df3375` |
  | `6bd909a` | `309d599` |
  | `34e49b2` | `400ed2e` |
  | `18eab00` | `36e949c` |
  | `429d645` | `b4d2e7e` |
  | `fb50256` | `4b25df6` |
  | `fa266d2` | `cee19da` |
  | `d5b7517` | `dbd9a78` |
  | `0423ad1` | `a5589d1` |
  | `3e4ec71` | `d02d922` |
  | `fc28bc6` | `95e2d44` |
  | `39e357d` | `8e272cd` |
  | `d8d5704` | `9e57647` |

## What this is not

Picks are never published before kickoff. Nothing here is a recommendation to bet. The record is reported with
sample sizes and confidence intervals because, over a season, win-loss alone cannot distinguish skill from
noise; the measure that matters is closing-line value.

Published by theRoodest (GitHub). The only genuine copy of the record page is https://theroodest.github.io/odds-record/.

21+ only, where legal. Gambling problem? Call 1-800-GAMBLER. Information and entertainment, not financial advice.
