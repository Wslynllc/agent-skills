<!-- BEGIN Wslynllc fork section. Not upstream text; keep it above the upstream file so syncs from openclaw/agent-skills stay easy. -->
# Wslynllc fork of openclaw/agent-skills

Read this section first, then the upstream `AGENTS.md` below it, which is unchanged.

- Shared standards win: `Wslynllc/project-standards` (`README.md`, `Owner approval.md`, `Delivery gates.md`, `CI and runners.md`). This section adds only this fork's values; where the upstream text below differs, the standards win.
- Merging deploys nothing. The only workflow, `.github/workflows/validate.yml`, is defined to run on pull requests and pushes to `main`, but no runs were observed on this fork (2026-11-18; cause unknown), so no check will report on your PR: run the offline check below yourself and report its output. No deploy workflow, environment or flag exists. Installing skills on a machine is a separate, manual `scripts/install-skills` run. How downstream repos sync from here is unknown (not in this tree).
- Owner tap (`rkroelin-yes`): only `/.github/` (workflows and `.github/CODEOWNERS` itself), as `.github/CODEOWNERS` defines. Skills, scripts and docs merge after independent agent review.
- Offline check: no Makefile. Run the commands in `README.md` "Validate", which mirror `.github/workflows/validate.yml` (PyYAML from `requirements-dev.txt`). Create the venv outside the checkout, for example under `$TMPDIR`, not README's in-repo `.venv/`: `skills/autoreview/scripts/autoreview` ignores PATH entries inside the repo (`find_command`), so an in-repo venv makes `--self-test-opencode-isolation` and `test_self_test_shortcut_runs_deterministic_checks` fail with "executable not found". `validate.yml` targets `ubuntu-latest` and `windows-latest`, so scripts must work on both.
- Generated files: none in this tree. Never edit downstream vendored copies by hand (upstream rule below).
- Before a push: `trufflehog git file://$PWD --since-commit origin/main --branch HEAD --no-update --no-verification --fail` must find nothing in your commits. A whole-history scan reports unverified placeholder-URL hits in upstream's `skills/autoreview/tests/test_autoreview_hardening.py` fixtures (count depends on scan scope), so scan only your range. This repository is public: keep private hostnames, accounts and URLs out of every file, this one included.
- Upstream: `openclaw/agent-skills` is canonical. Fork-only content is limited to `.github/CODEOWNERS` and this section; keep other changes small and upstreamable so syncs stay clean.
- Kanban lane board: none dedicated to this repository.

Where to read before changing things:

- `README.md`: included skills, install, "Validate" and "Editing Rules".
- `VISION.md`: what belongs in the catalog and what does not; read before adding a skill.
- `skills/<name>/SKILL.md`: each skill's contract. `skills/autoreview/AGENTS.md` adds rules for that skill, and `skills/beam/README.md` documents beam.
- `scripts/`: `install-skills` and `validate-skills` with their `*.test.py`. `skills.sh.json` groups skills for skills.sh.
- Related repositories: `openclaw/agent-skills` (upstream) and `Wslynllc/project-standards`. Which downstream repos vendor these skills is unknown.
<!-- END Wslynllc fork section. Upstream text follows unchanged. -->

# AGENTS.md

Public shared skills for agent workflows.

## Rules

- Canonical shared skills live under `skills/<name>/SKILL.md`.
- Keep repo-specific workflows out unless they are useful as public examples.
- Keep secrets, private hostnames, private account IDs, and private URLs out.
- Skill descriptions: short trigger phrase, not full documentation.
- Skill bodies: operational, terse, current.
- Helper scripts belong under `skills/<name>/scripts/`.
- Validate after edits: `scripts/validate-skills`.
- Do not edit generated/vendor copies in downstream repos; update here, then sync.

## Layout

- `skills/autoreview`: shared closeout/code-review helper.
- `skills/beam`: redacted read-only coding-session publication.
- `skills/crabbox`: shared Crabbox/Testbox remote validation workflow.
