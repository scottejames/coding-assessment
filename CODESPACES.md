<p align="center">
  <img src="logo.svg" alt="Coding Assessment" width="480">
</p>

# Using GitHub Codespaces

This is the **no-install option**: write and run your solution entirely
in your browser, in a ready-to-go environment with Python and Java
already set up. It's a genuine alternative to installing anything on
your own machine — if you'd rather work locally instead, see
[LOCAL_SETUP.md](LOCAL_SETUP.md).

All you need is a GitHub account and a browser.

## Step 1 — get your own copy

Go directly to the problem's `/generate` link — for example, for Pair
the Numbers:

**`https://github.com/scottejames/pair-the-numbers-starter/generate`**

(Swap `pair-the-numbers-starter` for whichever problem you're doing —
each repo listed in [README.md](README.md) supports this the same way.)

On the form that appears:
1. Leave "Owner" as your own account.
2. Give it any name you like (e.g. `my-solution`).
3. Select **Private**.
4. Click the green **Create repository** button.

You now have your own repository, completely independent of ours — not
a fork, nothing connecting it back to us. This is the repo you'll work
in.

## Step 2 — open it in a codespace

1. On *your new repo's* page, click the green **Code** button.
2. Click the **Codespaces** tab.
3. Click **Create codespace on master**.
4. Wait for it to build (a minute or so, first time only). A full VS
   Code opens right in your browser tab, already showing your files.

## Step 3 — do the problem

Open the solution file named in the repo's `README.md` (e.g.
`python/pair_numbers.py` or `java/src/PairNumbers.java`), write your
solution, and run the test script from the built-in terminal as you go:

```bash
cd python                # or java
./scripts/test.sh
```

*(Note: Copilot suggestions are turned off by default in this
environment, in line with the no-AI-tools policy in
[README.md](README.md).)*

## Step 4 — submit it

There's no separate submission step — submitting *is* pushing your
commits to the repo you created in Step 1, then letting us know it's
there:

1. In VS Code's left sidebar, click the **Source Control** icon, stage
   your changes, write a commit message, click **Commit**, then
   **Sync Changes** — or just use the terminal: `git add .`, `git commit
   -m "..."`, `git push`.
2. Since the repo is **private**, add the GitHub username you were
   given under your repo's **Settings → Collaborators → Add people**,
   or just send us the repo's URL.

That's it — nothing to build, zip, or upload separately.

## If the codespace seems stuck

The first build can genuinely take a couple of minutes — it's
installing Python and Java from scratch. A blank screen for 2–4 minutes
isn't necessarily broken. If it's been much longer than that, or shows
as `Failed` on [github.com/codespaces](https://github.com/codespaces),
delete it there and create a fresh one.
