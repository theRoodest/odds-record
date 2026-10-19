# Odds Generator — public track record

This repository is the tamper-evidence for a sports-betting value finder's daily reports. The pipeline itself
is private. What is public here:

- `hashes/<date>.sha256`: the SHA-256 of every report written on that date, committed the same morning,
  before any of the games start. A hash proves the report existed, unchanged, at that commit's timestamp.
- `source-commits.txt`: for each date, the commit in the private source repository that holds the reports.
- `reports/`: the report files themselves, released 7 days after their date, once every game in them has
  started. Verify any released file against its morning hash:

  ```
  shasum -a 256 -c hashes/2026-10-18.sha256
  ```

- A record page (closing-line value, ROI, hit rate, sample sizes and confidence intervals per market) will be
  published here once built.

## What this is not

Picks are never published before kickoff. Nothing here is a recommendation to bet. The record is reported with
sample sizes and confidence intervals because, over a season, win-loss alone cannot distinguish skill from
noise; the measure that matters is closing-line value.

21+ only, where legal. Gambling problem? Call 1-800-GAMBLER. Information and entertainment, not financial advice.
