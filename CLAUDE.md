# CLAUDE.md — fork `theim` di linkedin-skills

> Fork di [sergebulaev/linkedin-skills](https://github.com/sergebulaev/linkedin-skills) adattato per Sandro Vespucci e The I'm. **Il fork è pubblico**: nessun dato personale qui dentro. Voce e Story Bank vivono nel vault privato (`references/strato-vault.md`). Ramo di lavoro: `theim`; `main` resta allineato a `upstream` per poter assorbire gli aggiornamenti.
> Lavoro in corso (seconda sessione): italianizzazione di regole di voce, scrub-rules e formule di hook.

## Versioning

- Single source of truth: `.claude-plugin/plugin.json`,
  `.claude-plugin/marketplace.json`, `.codex-plugin/plugin.json`, and
  `.agents/plugins/marketplace.json`. Plugin manifests must always match on
  package name and version; marketplace entries must point to the same package;
  author, license, homepage, and the public skill-bundle description must stay
  aligned.
- Keep `CLAUDE.md` and `AGENTS.md` aligned when changing shared project
  rules. Claude-specific workflow details belong here; Codex-specific
  workflow details belong in `AGENTS.md`.
- Codex marketplace install uses `.codex-marketplace/linkedin-skills/`.
  Do not edit that generated package by hand. Update the root files first,
  then run `python3 scripts/sync_codex_marketplace.py`.
- **Default: bump the PATCH segment (3rd level, `0.0.X`).** This is the
  automatic behavior for every shippable commit, regardless of how
  large the diff feels. Skill renames, lib API breaks, new features:
  still PATCH by default.
- Only bump MINOR or MAJOR when **the user explicitly asks** for a
  higher rank ("это minor", "make it 2.0", "bump major"). Do not
  promote on your own initiative even if semver textbook says so.
- After bumping, two steps are required:
  1. Tag the commit: `git tag -a v<X.Y.Z> -m "..."` + `git push origin v<X.Y.Z>`
  2. **Publish a GitHub Release** for the tag: `gh release create v<X.Y.Z> --title "v<X.Y.Z>" --notes "<changelog>" --latest`
  A tag alone does NOT update the README release badge or the
  Releases page. The shields.io badge reads from the Releases API,
  not from raw tags. Skipping step 2 leaves the badge stale.

## Commits

- Primary author **must** be Sergey: every `git commit` needs
  `--author="Sergey Bulaev <s@bulaev.org>"`. The harness defaults to the
  Claude identity if you forget; verify with
  `git log -1 --format='%an <%ae>'` before pushing.
- Co-author trailer (`Co-Authored-By: Claude ...`) is fine and welcomed.
- Verify locally before push: build never breaks, no broken refs in
  `SKILL.md`, library smoke import passes.

## Skill bundle invariants

- **Exactly 12 skills.** Adding requires merging or splitting elsewhere
  to stay at 12. The number is announced in plugin manifests and the README.
- **Frontmatter `description:` target ≤ 400 chars** (some bundle-heavy
  skills land slightly higher when their scope is genuinely broad — keep
  under 510). Always include a "Not for X (use Y)" disambiguation
  sentinel when the skill overlaps with a sibling.
- **No em dashes anywhere in `description:` fields.** Em dashes in body
  prose are allowed for table separators and list dividers only.
- **Skill names are public surface.** Renaming a skill is a major
  version bump and requires updating: `.codex-plugin/plugin.json`,
  `.agents/plugins/marketplace.json`, `.claude-plugin/plugin.json`,
  `.claude-plugin/marketplace.json`, root `SKILL.md` bundle list,
  README skill table, every
  `linkedin-<name>` cross-reference in sibling SKILL.md files.

## Voice rules + reference layout

- Canonical voice rules live at root `references/voice-rules.md`.
  Skill-local "Hard rules" sections must only contain skill-specific
  overrides (char ranges, threading rules, format constraints) and start
  with: `Global voice rules: see root SKILL.md §Voice rules.`
- Other root-level references shared across skills:
  `references/hook-formulas.md` (20 canonical formulas),
  `references/algorithm-heuristics.md`, and
  `references/untrusted-content.md` (the data-not-instructions rule for every
  skill that reads LinkedIn through the browser; keep the per-skill "Untrusted content"
  sections pointing at it).
- Skill-local references live in `skills/<skill>/references/`. Cite from
  the skill with bare `references/X.md`. Cite root from skills with
  `../../references/X.md`.
- `linkedin-humanizer` has `sub-skills/` for folded-in workflows
  (post-audit, emoji-detector, detector-tester, rules-explainer) and
  `scripts/` for runnable tools. Don't duplicate this pattern in other
  skills without a clear reason.

## .claude/skills mirror

- `.claude/skills/<name>` is a **relative symlink** to `../../skills/<name>`, one per
  skill. Claude Code discovers project skills at `.claude/skills/`, while the bundle
  keeps them at `skills/` for the agentskills.io and plugin layouts, so a plain
  `git clone` used as a working directory activates nothing without this.
- `skills/` stays the single source of truth. The mirror holds no content, so there is
  nothing to sync and nothing that can drift. Relative references still resolve because
  symlinks resolve physically: `../../references/` from a mirrored skill lands on the
  repo root, not inside `.claude/`.
- **Adding or renaming a skill means adding or renaming its symlink.** A missing one is
  silent: the skill simply does not appear for anyone who cloned the repo.
- The mirror is Claude-specific and is deliberately not copied into the Codex package.

## Layer separation

Niente layer a pagamento (Apify, Publora, Pixfaro sono stati tolti con `lib/`).

- **Lettura e pubblicazione:** browser interno di Claude, `references/strato-browser.md`.
  Una conferma esplicita per ogni oggetto pubblicato, niente programmazione, niente raffiche.
- **Immagini:** composizione HTML → render PNG nel look del brand pubblico,
  `references/strato-immagini.md`.
- **Modello dell'utente:** due voci (Sandro, The I'm) e una Story Bank nel vault,
  `references/strato-vault.md`. `references/voice-profile.md` e `references/story-bank.md`
  sono solo puntatori e **non vanno mai riempiti** in questo repo.

## testing/ is gitignored

- `testing/` is the local scratch directory: API keys, sample API
  responses, validation reports, integration scripts.
- Never write secrets above `testing/` (the rest of the repo is public).
- The `.gitignore` rule for `testing/` is load-bearing; do not change.

## Validation before push

Run from repo root:

```bash
ls skills/ | wc -l        # must equal 9
python3 scripts/check_frontmatter.py
python3 scripts/check_no_secrets.py
python3 -m unittest discover -s tests
grep -nE '^description:' skills/*/SKILL.md SKILL.md | grep -E '—|–'   # must be empty
grep -rnE 'filled: yes' references/   # must be empty: user data never lives in the fork
```

If any of these fail, do not push.
