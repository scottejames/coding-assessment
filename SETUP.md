# Codespaces setup — working notes

This is a staging document for adding [GitHub
Codespaces](https://github.com/features/codespaces) support to the
series, so a student can write and run their solution entirely in the
browser, with nothing to install locally. It's **not candidate-facing
yet** — `README.md` in this repo and in each `-starter` repo still
describe the local install/clone flow only, on purpose, until we're
happy with this.

**Status: rolled out to `pair-the-numbers-starter` only**, as a first
test. Nothing else has been touched.

---

## Why

The local setup flow (install Python/Java/Git, clone, detach the
remote, create a new repo, wire up a remote, push) is the single
biggest source of friction for students who don't already have a dev
environment ready to go. Codespaces collapses most of that: a student
with just a GitHub account and a browser gets a real VS Code, with the
right language tools already installed, running against the repo
already checked out — no install step at all.

It doesn't remove *every* step — they still need to redirect their work
to a private repo of their own before pushing (see below) — but that's
now a couple of terminal commands inside the browser, not a local
toolchain to assemble first.

## What we added

`.devcontainer/devcontainer.json` in `pair-the-numbers-starter`:

- **Base image:** `mcr.microsoft.com/devcontainers/base:ubuntu` — a
  small, generic Ubuntu image, not the much larger "universal" image
  Codespaces defaults to, so the container builds faster.
- **Features:** the officially maintained `python` and `java`
  dev container features, installing Python 3.12 and a JDK 21. Both
  are present regardless of which language the student picks — we
  don't know in advance.
- **VS Code extensions:** the Python extension and the Java extension
  pack are pre-installed, so there's no "do you want to install an
  extension?" prompt to get in the way.
- **`postCreateCommand`:** prints `python3 --version` and `java
  -version` the moment the container finishes building, right in the
  terminal — an immediate, visible confirmation that both languages are
  actually there, before the student's typed a single line of their
  own.

## The student flow this enables

1. Open the repo on github.com → **Code** button → **Codespaces** tab →
   **Create codespace on master**. (Deliberately *not* forking first —
   forks of a public repo are always public, which would make the
   student's solution visible to everyone. Creating a codespace
   directly on our public repo works fine without write access, and
   nudges them straight into step 3 below.)
2. Wait for the container to build (first time only — a minute or so).
   A real VS Code opens in the browser tab, already showing the repo.
3. In the built-in terminal, redirect to a repo of their own — same
   commands as the local flow, just run here instead:
   ```bash
   git remote remove origin
   gh repo create my-pair-the-numbers-solution --private --source=. --remote=origin --push
   ```
   (`gh` comes preinstalled in every codespace by default, so this is
   actually simpler here than on a fresh local machine.)
4. Implement the solution, run `./scripts/test.sh` in the terminal, and
   commit/push from VS Code's Source Control panel (or the terminal) as
   normal.

## Testing checklist

Could you try these on `pair-the-numbers-starter` and we'll note the
results here?

- [ ] Open a codespace on `pair-the-numbers-starter` from github.com
- [ ] `postCreateCommand` output shows a real Python version and a real
      Java version, no errors
- [ ] `cd python && ./scripts/test.sh` runs and prints `NOT IMPLEMENTED`
      for all 19 cases (i.e. it *runs*, we're not checking it passes)
- [ ] `cd java && ./scripts/test.sh` compiles and runs likewise
- [ ] The `git remote remove origin` + `gh repo create ... --push` step
      actually lands the code in a new repo under your account
- [ ] Note how long the first build took
- [ ] Note whether the Python/Java VS Code extensions were active
      without any manual prompt

## Known caveats

- **Free tier limits.** Personal GitHub accounts get a limited number
  of free Codespaces core-hours per month. Fine for occasional one-hour
  sessions; worth keeping in mind if this scales up a lot.
- **New/unverified accounts.** GitHub's anti-abuse checks occasionally
  block a very new or unverified account from creating a codespace
  until they verify (e.g. add a phone number). Nothing we can route
  around centrally — worth a line in candidate-facing instructions once
  we get there.

## Next steps

- [ ] Run through the testing checklist above
- [ ] Decide whether to copy `.devcontainer/devcontainer.json` to the
      other four `-starter` repos
- [ ] Decide how (and whether) to present this in each repo's
      `README.md` — likely as the recommended fast path, with the
      existing local-install instructions kept as a fallback for anyone
      who'd rather work locally
