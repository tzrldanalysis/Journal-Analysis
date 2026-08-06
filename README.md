# Journal Analysis

Daily and weekly financial intelligence briefs generated from newspaper editions (WSJ, FT).

## Structure

```
daily-briefs/
  YYYY/
    MM/
      YYYY-MM-DD-[pub].md

weekly-briefs/
  YYYY/
    YYYY-Www-[weekstart]-to-[weekend].md
```

- **daily-briefs**: one file per publication per trading day. Each contains 14 sections (themes, markets, geopolitics, business, steel-man, priors, forward-looking implications, absent stories, Europe watch, counterparty risk, cross-publication delta, one-to-watch, research questions) plus a machine-readable `[DATA TAGS]` block. Generated automatically each weekday morning from the incoming PDF edition. Prompt: `PROMPT` in `prompts.txt`.
- **weekly-briefs**: one file per trading week, synthesising that week's daily-briefs (both WSJ and FT). Tracks theme arcs across days, scores forward-looking calls against what actually happened, and maintains a live ticker scorecard against the Ticker Tracker log. Includes a `[WEEKLY DATA TAGS]` block for future monthly roll-up. Generated automatically each Saturday from the completed Mon–Fri week. Prompt: `PROMPT_WEEKLY` in `prompts_weekly.txt`. Skips generation if that week's file already exists (idempotent).

## Ticker Tracker

Every ticker call (`TICKERS_LONG` / `TICKERS_SHORT`) logged in daily-briefs DATA TAGS is tracked in `Ticker_Tracker.xlsx` (kept locally in the Financial Journals folder, not committed here) — entry price (live-quoted or article-stated, disclosed either way), current price, and direction-adjusted return % since entry. Updated as part of each weekly-briefs run.
