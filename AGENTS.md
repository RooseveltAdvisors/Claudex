# Codex project instructions

Read and follow [CLAUDE.md](CLAUDE.md) as the authoritative repository guide. Keep Bash and PowerShell behavior aligned, preserve the documented trust boundaries, and add a regression test for every compatibility fix.

## Backpass

Session memory mining for this repo is configured in `.backpassrc.json`; the `cloneRoots`/`worktreeGlobs` paths are gpu host specific. Run `bunx backpass@latest scan --force --json` then `bunx backpass@latest`.
