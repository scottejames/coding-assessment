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

It doesn't remove *every* step — they still need their own copy of the
repo, and a way to hand the finished result back to us — but both of
those are now a couple of clicks, not a local toolchain to assemble
first.

## What we added

**1. `.devcontainer/devcontainer.json` in `pair-the-numbers-starter`:**

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

**2. `pair-the-numbers-starter` is now marked as a GitHub "template
repository"** (Settings → General → Template repository, already
switched on — done via `gh repo edit ... --template`). This is what
makes the "no forking" flow below possible: a repository created *from*
a template has **no fork relationship to the original at all** — no
shared history, no "forked from" label, and critically, **it can be
private even though the template itself is public.** A plain GitHub
fork can't do that last part, which is why we're using this instead of
forking.

## The exact student flow

**Step 1 — get your own copy (not a fork).**

1. Go directly to:
   `https://github.com/scottejames/pair-the-numbers-starter/generate`
   (this is GitHub's direct link for "create a repository from this
   template" — there is a **Use this template** button on the repo
   page too, but it isn't next to **Code** where you'd expect, so the
   direct link is the more reliable thing to give students).
2. On the form that appears: leave "Owner" as your own account, type a
   repository name (anything — e.g. `my-pair-the-numbers-solution`),
   and — importantly — select **Private**.
3. Click the green **Create repository** button.

You now have your own repository, e.g.
`github.com/<your-username>/my-pair-the-numbers-solution`, containing
everything from the starter repo, fully private, with no connection
back to ours. This is the repo you'll work in for everything below.

**Step 2 — open it in a codespace.**

1. On *your new repo's* page, click the green **Code** button.
2. In the dropdown, click the **Codespaces** tab.
3. Click **Create codespace on master**.
4. Wait for it to build (a minute or so, first time only). A full VS
   Code opens right in the browser tab, already showing your files,
   with a terminal at the bottom printing the Python/Java version check
   from `postCreateCommand`.

**Step 3 — do the problem.**

Open the solution file named in `README.md` (e.g.
`python/pair_numbers.py`), write your solution, and run
`./scripts/test.sh` in the built-in terminal as you go — exactly as
described in that repo's own `README.md`.

**Step 4 — "submit" it.**

There's no separate submission step or portal — submitting *is*
pushing your commits to the private repo you created in Step 1, then
letting us know it's there:

1. In VS Code's left sidebar, click the **Source Control** icon (looks
   like three connected dots/branches). Stage your changes (the `+`
   next to each file, or "Stage All Changes"), type a commit message,
   click the ✓ **Commit** button, then click **Sync Changes** (this
   does the push). Or just use the terminal: `git add .`, `git commit
   -m "..."`, `git push` — whichever you prefer.
2. Since the repo is **private**, we can't see it until you either:
   - go to your repo's **Settings → Collaborators → Add people**, and
     add the GitHub username you were given, **or**
   - just reply/send us the repo's URL and we'll request access.
3. That's it — nothing to build, zip, or upload separately.

## Testing checklist

Could you try these end-to-end and we'll note the results here?

- [x] The `/generate` link → "Create a new repository" actually
      produces a private, fork-free repo under your account (confirmed
      — the on-page "Use this template" button exists but isn't next to
      "Code" where you'd expect it, so we're using the direct link
      instead)
- [ ] Codespace builds on *that* new repo without errors
- [ ] `postCreateCommand` output shows a real Python version and a real
      Java version, no errors
- [ ] `cd python && ./scripts/test.sh` runs and prints `NOT IMPLEMENTED`
      for all 19 cases (i.e. it *runs*, we're not checking it passes)
- [ ] `cd java && ./scripts/test.sh` compiles and runs likewise
- [ ] A commit made in the codespace successfully pushes back to your
      new repo (check it shows up on github.com)
- [ ] Note how long the first container build took
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
      other four `-starter` repos, and mark each as a template
      repository the same way (`gh repo edit <repo> --template`)
- [ ] Decide how (and whether) to present this in each repo's
      `README.md` — likely as the recommended fast path, with the
      existing local-install instructions kept as a fallback for anyone
      who'd rather work locally
