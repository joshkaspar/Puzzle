# About this fork

This is joshkaspar's fork of [sidhant947/puzzle](https://github.com/sidhant947/puzzle).
`README.md` is the main project's own, left as is so merges stay clean. This file covers
what the fork adds.

## Branches

| Branch | What it is |
|---|---|
| `main` | An exact copy of the main project. Never commit to it directly. |
| `train-tracks` | **Retired 2026-11-22.** `main` plus the games as they were before they moved to [joshkaspar/kaspar-puzzles](https://github.com/joshkaspar/kaspar-puzzles). Kept so image tags built from it stay reproducible. Don't develop here. |

The games, Train Tracks and Rack & Resonance, now live in
[joshkaspar/kaspar-puzzles](https://github.com/joshkaspar/kaspar-puzzles), with their
history. This fork is back to being a plain mirror: puzzle-docker builds the app from a
commit of `main` and adds the games from kaspar-puzzles. See
[puzzle-docker's README](https://github.com/joshkaspar/puzzle-docker#the-fork).

Remotes: `origin` is this fork, `upstream` is the main project.

## Taking the main project's updates

```sh
git fetch upstream
git checkout main && git merge --ff-only upstream/main && git push origin main
```

`main` has no commits of its own, so the first merge is always a fast-forward. Review
what came in before deploying.

## Building and deploying

See [puzzle-docker](https://github.com/joshkaspar/puzzle-docker): it builds the app from
`PUZZLE_REF` (a commit of `main`) and the games from `GAMES_REF`. The server (Zuul) is
documented in the private `zuul-unraid` repo under `apps/puzzle/`.

Live at `https://puzzles.kaspar.casa`, with Train Tracks at `/tracks/` and Rack & Resonance
at `/rack/`.
