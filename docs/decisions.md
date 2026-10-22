# Decision Log

> Key project decisions: what was decided, why, and which alternatives were discarded.
> Most recent at the bottom. Each decision has an ID so it can be referenced (e.g., "see D-004").

---

## D-001 · Local first, cloud later
- **Date:** 2026-10-22 · **Phase:** 0
- **Decision:** Develop everything locally and move to Google Cloud in Phase 6.
- **Why:** Learn each layer separately (data, model, app, cloud) instead of debugging several at once.
- **Discarded alternatives:** Working in the cloud from day one (more complexity and cost risk while learning the basics).

## D-002 · venv as the environment manager
- **Date:** 2026-10-22 · **Phase:** 0
- **Decision:** Use `venv` + `pip`.
- **Why:** Ships with Python, is the standard, and fits naturally with `requirements.txt` and GitHub Actions.
- **Discarded alternatives:**
  - *conda:* Heavier; mixing conda and pip can cause conflicts; less common in deployments.
  - *uv:* Very fast and modern, but adds an extra tool during Phase 0.

## D-003 · Python 3.14
- **Date:** 2026-10-22 · **Phase:** 0
- **Decision:** Use Python 3.14.6, the version already installed.
- **Why:** A smoke test installed and imported the full stack without errors (fastf1 3.8.3, pandas 2.3.3, xgboost 3.4.1, duckdb, pyarrow, scikit-learn, streamlit, plotly). Evidence-based decision rather than an assumption.
- **Discarded alternatives:** Installing Python 3.12 side by side (maximum compatibility, but unnecessary according to the test).
- **Fallback plan:** If any library fails on 3.14 (e.g., during deployment), recreate the environment with 3.12.

## D-004 · `requirements.txt` with pinned direct dependencies
- **Date:** 2026-10-22 · **Phase:** 0
- **Decision:** Hand-write only the 9 direct dependencies, each pinned to an exact version (`==`).
- **Why:** Readable (every line has a clear purpose) and portable across operating systems; pip resolves transitive dependencies on each platform.
- **Discarded alternatives:**
  - *`pip freeze`:* Pins 100+ packages, including Windows-only ones (`pywinpty`) that would break installation on Linux (GitHub Actions, Streamlit Cloud).
  - *Lock file (`requirements.in` + pip-tools/uv):* Full reproducibility, but adds complexity now; with pip-tools on Windows the lock file could also end up Windows-specific (requires a universal option such as `uv --universal`).
- **Revisit in:** Phase 6, if reproducibility issues appear.

## D-005 · What Git ignores
- **Date:** 2026-10-22 · **Phase:** 0
- **Decision:**
  - Ignore `/data/` (anchored to the repo root). The FastF1 cache will live in `data/cache/`.
  - Safety net by file extension: `*.parquet`, `*.duckdb`, `*.duckdb.wal`, `*.ff1pkl`.
  - Ignore `.vscode/` (it only contains personal editor preferences).
  - Data folders are created by code instead of being kept in Git with `.gitkeep`.
- **Why:** Heavy data does not belong in the repo; a single place for data and a single rule that covers it.
- **Lesson learned:** The pattern `data/` (without a leading `/`) also ignored `src/data/`. Detected with `git check-ignore -v` and fixed by anchoring the pattern as `/data/`.

## D-006 · Conventional Commits
- **Date:** 2026-10-22 · **Phase:** 0
- **Decision:** Prefix commit messages with `feat:`, `fix:`, `docs:`, `chore:`, `refactor:` or `test:`.
- **Why:** Clean, readable history; a common industry practice.

## D-007 · Repository content in English
- **Date:** 2026-10-22 · **Phase:** 0
- **Decision:** Write all repository content in English: code, comments, README and documentation.
- **Why:** The repo is a public portfolio project; English makes it accessible to recruiters and developers anywhere.
- **Discarded alternatives:** Keeping some docs in Spanish (mixed languages in a public repo look inconsistent).
- **Note:** Personal learning notes stay in Spanish outside the repo.