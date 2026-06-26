# Contributing to Suspicious Activity Tracker

Thanks for considering a contribution. This project favors small, real,
tested changes over large speculative ones — see
`docs/architecture/future_work.md` for the explicit list of what's
scoped out and why; that list is also the best place to look for ideas
on what to contribute.

## Before you start

- Read `docs/guides/developer_guide.md` for the repository layout and
  module boundaries.
- Check `docs/architecture/future_work.md` to see if what you're
  planning is already scoped/sequenced, or deliberately excluded with a
  documented reason.
- For anything nontrivial, open an issue first to discuss the approach
  before writing code.

## Development setup

See `docs/guides/installation.md` — the "AI core only" or "Backend +
lite AI core" setups are sufficient for most contributions and avoid the
multi-gigabyte torch/ultralytics install.

## Pull request checklist

- [ ] New logic has real tests — synthetic data for AI core changes
      (see `tests/ai/synthetic_data.py`), real in-memory-DB integration
      tests for backend changes (see `backend/tests/test_integration_full_flow.py`
      for the pattern).
- [ ] `JWT_SECRET_KEY=test PYTHONPATH=. pytest -v` passes.
- [ ] `ruff check ai_models backend` is clean.
- [ ] If you touched the frontend: `npm run type-check && npm run lint && npm run build` all pass.
- [ ] If you added a new SQLAlchemy model or column: a real Alembic
      migration is included (`alembic revision --autogenerate`), and
      you've reviewed the generated migration for correctness.
- [ ] If you added a new dependency: it's pinned to an exact version in
      the relevant `requirements*.txt` or `package.json`, not a loose
      range — see `docs/guides/troubleshooting.md`'s FastAPI/instrumentator
      incompatibility for why exact pins matter here.
- [ ] Docstrings explain *why*, not just *what*, for any non-obvious
      design decision — match the existing style in e.g.
      `ai_models/anomaly/isolation_forest.py`.

## Commit messages

No strict format enforced, but please write a real sentence describing
the change's effect, not just a restatement of the diff.

## Code of conduct

Be direct and substantive in code review; be respectful in tone. We'd
rather have a contributor point out a real bug bluntly than soften
useful feedback into vagueness.
