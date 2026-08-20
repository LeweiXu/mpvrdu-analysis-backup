# mpvrdu results backup

Automatic daily snapshot of the **irreplaceable** mpvrdu artifacts. Everything here
cost days of H100 time or paid judge API calls; everything deliberately left out
regenerates for free.

## What's here

- `repo-results-cache/` — mirror of the repo's `results/cache/` (jsonl only):
  `predictions.jsonl` (generation) and `results.jsonl` (judged), per run_tag/task,
  plus retrieval/classifier side artifacts and the parser markdown cache.
- `student-results-cache/` — frozen snapshot of the H100 run that used to live in
  `~/mpvrdu_results/cache`. Merged into `repo-results-cache/` on 2026-08-20 and no
  longer updated; it is the only remaining copy of the smoke-* tags and of
  g1-reasoner-thinking (a failed experiment dropped from the working tree).
- `tables/` — the built CSVs and `all_tables.md`.

## What's NOT here, and why

- **Page renders** (`renders/**.png`, ~20 GB) — deterministic re-render from the PDFs
  at the run DPI. Costs CPU minutes, no GPU.
- **Model weights** (`.cache/`, ~14 GB) and **the dataset** (`.data/`) — re-download
  with `python -m ops.scripts.prestage --local --config ops/kaya/h100_main.json`.

## Restoring

Copy `repo-results-cache/` back over `results/cache/` in the repo (and
weights. Renders and any missing derived artifacts rebuild on the next run;
`python -m ops.build` regenerates the tables.
