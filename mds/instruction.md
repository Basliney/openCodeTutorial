Задача: добавь мои ограничения в глобальный `instructions` opencode, чтобы они применялись во всех проектах и для всех моделей.

Шаги:
1. Открой `~/.config/opencode/opencode.json` (если его нет — создай с `"$schema": "https://opencode.ai/config.json"`).
2. Создай файл `~/.config/opencode/rules/boundaries.md` с текстом ограничений ниже.
3. Добавь в `opencode.json`:
   "instructions": ["~/.config/opencode/rules/boundaries.md"]
   Если ключ уже есть — добавь путь к массиву, не перезаписывая существующие значения.
4. Не делай коммитов. Покажи итоговый конфиг и напомни перезапустить opencode.

Содержимое boundaries.md:

# Global boundaries

Hard boundaries for every project and every model. If a request conflicts with these rules, ask instead of proceeding.

## Git
- Commit only when the user explicitly asks; never auto-commit
- Never push / force-push unless explicitly asked
- Never rewrite history (reset --hard, rebase, commit --amend, filter-branch) on shared commits without approval
- Never delete or force-move branches without approval
- Do not modify .git/config, git hooks, or use --no-verify
- Before any commit: review git status + git diff, stage only intended files, never blind git add -A

## Destructive operations
- Never run rm -rf or any recursive delete without explicit confirmation
- Do not delete, truncate, or overwrite files outside the current task
- No git clean, mass renames/moves, or disk-wide deletes
- Prefer reversible operations; ask before anything hard to reverse

## Software installation
- Any software install only after explicit user permission: system packages (apt, dnf, pacman, brew), global npm/pip/cargo/go packages, binaries, plugins, IDE extensions, MCP servers, containers, etc.
- Propose the install command first, run only after approval
- If a dependency is needed for the task, ask — never install silently
- Do not remove or upgrade installed software without request
- Project-local installs (venv, local node_modules, npx) are allowed when the task requires them

## Secrets
- Never read, print, log, or commit secrets: .env*, keys, tokens, passwords
- Never write secrets into code, configs, logs, or commit messages
- If a task needs a secret, ask the user to provide it via environment variable

## Packages and infrastructure
- No package publish, deploy, DB migrations, or CI/CD edits without explicit request
- No system-wide/global installs or OS config changes without approval
- Do not upgrade dependencies or lockfiles unless the task requires it

## Scope and verification
- Minimal changes, strictly scoped to the task; no unrelated refactors
- Do not disable tests, linters, or type checks to make things pass
- Follow repository conventions
- Run lint, typecheck, and tests (if available) after changes
