# Vision

RooseveltAdvisors/Claudex is the house fork of BeamoINT/Claudex, the open source compatibility layer that runs Codex GPT models and native Claude models through the Claude Code interface.
Upstream owns that product and its community; this fork exists for a narrower reason: fleet installations must come from this fork, because the upstream BeamoINT Homebrew tap alone is not sufficient.
The pain it removes is waiting on someone else's release cadence: when the fleet's skill libraries outgrew upstream's published cache safety limits, the fix could not wait for an upstream release.
So the fork is a thin, pinned delta on top of upstream plus its own release line, kept as close to upstream as the fleet's needs allow.
It serves the RooseveltAdvisors fleet: the machines and agents that install Claudex from this fork's releases.
It deliberately does not serve a second community: end users, package manager channels, discussions, and the roadmap belong to upstream.

## What it carries beyond upstream

The one product change is room: the skill bridge's published cache limits rise from upstream's 4096 files, 16 MB per file, and 64 MB per tree to 16384 files, 32 MB per file, and 256 MB per tree, because RooseveltAdvisors fleet skill libraries need room for larger published caches.
A regression test pins both sets of numbers, so a merge with upstream cannot silently erase or widen the delta.
The fork cuts its own semantic version releases, such as v1.6.3, and points its changelog compare links at this repository for new versions.
House infrastructure travels with it: a `.github/dependabot.yml` updating npm and GitHub Actions dependencies weekly, maintained action digests, and the small workflow and documentation check adjustments the fork's repository settings require.
Upstream maintainer local artifacts that do not travel, such as the storage hygiene section of the agent guide and the Cursor and `.ai` memory files, are removed here rather than carried.

## What it must never diverge on

The delta stays minimal and raise only: limits go up, never down, and every other upstream safety guard stays exactly as upstream set it.
When upstream raises its own limits higher, the fork adopts upstream's numbers instead of keeping its own.
Every binding design rule from the agent guide holds here unchanged: never modify the signed Claude Code executable, keep `~/.config/claudex` separate from normal Claude Code state, let Codex own login and logout, keep secrets out of arguments, logs, caches, tests, and Git, bind the compatibility service to loopback only, verify every downloaded asset's digest, preserve unknown arguments exactly, keep Bash and PowerShell behavior aligned, and add a regression test before considering a bug fixed.
Fleet work ships to this origin and nowhere else; the fleet never opens pull requests or issues against BeamoINT upstream.
Changes to authentication, credential handling, downloaded binaries, or provider routing keep upstream's maintainer review discipline, never a fork shortcut.

## Non goals

- No product features developed only here that belong in upstream's product.
- No weakening of trust boundaries, digest verification, or safety limits.
- No second community surface, release channel, or roadmap.

## Done well, one year out

The merge base with upstream main stays recent, and the whole delta still fits in one short review: the limit raise, its test, the release plumbing, and the house infrastructure files.
Every fork release is upstream's release plus exactly the pinned delta and nothing more, and fleet installations keep working from this fork alone.
A merge from upstream stays routine, boring, and free of conflicts, because the fork never touches what upstream owns.
