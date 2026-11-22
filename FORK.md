# About this fork

This is joshkaspar's fork of [sidhant947/puzzle](https://github.com/sidhant947/puzzle).
`README.md` is the main project's own, left as is so merges stay clean. This file covers
what the fork adds.

## Branches

| Branch | What it is |
|---|---|
| `main` | An exact copy of the main project. Never commit to it directly. |
| `train-tracks` | `main` plus the fork's own games: Train Tracks ([`tools/tracks/`](tools/tracks/README.md), `web/tracks/`) and Rack & Resonance ([`tools/rack/`](tools/rack/README.md), `web/rack/`). This is what gets built and deployed. |

Larger changes to a game start on a branch of their own (for example `tracks-tutorial`
or `rack-and-resonance`), get tested, then fast-forward into `train-tracks`.

The games are planned to move to their own repo, `kaspar-puzzles`
(see [`tools/SPLIT-PLAN.md`](tools/SPLIT-PLAN.md)).

Remotes: `origin` is this fork, `upstream` is the main project.

## Taking the main project's updates

```sh
git fetch upstream
git checkout main && git merge --ff-only upstream/main && git push origin main
git checkout train-tracks && git merge main && git push origin train-tracks
```

`main` has no commits of its own, so the first merge is always a fast-forward. Review
what came in before deploying.

## Building and deploying

The app is never built on the dev machine, which has no Flutter. The game pages are:
each game's `build.sh` needs only the plain Dart SDK (installed at
`~/.local/share/dart-sdk`), and its output (`web/<game>/index.html`) is committed. The web
build and the image come from [joshkaspar/puzzle-docker](https://github.com/joshkaspar/puzzle-docker):
its `Dockerfile` pins a commit of `train-tracks` (`ARG PUZZLE_REF`), and GitHub Actions
builds and publishes the image when that pin changes. See its README for the release
steps. The server it runs on (Zuul) is documented in the private `zuul-unraid` repo
under `apps/puzzle/`.

Live at `https://puzzles.kaspar.casa`, with Train Tracks at `/tracks/` and Rack & Resonance
at `/rack/`.
