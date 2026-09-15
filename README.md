# Coding Assessment

Welcome! This repo is the index for our take-home coding assessment. Each
problem lives in its own repository (linked below) — this page just tells
you what to expect, in what order to tackle things, and how to get set
up.

You'll pick **one problem at a time**, work through it in **either
Python or Java** (your choice — both are graded identically), and end up
pushing your solution to a repository of your own. Nothing here needs to
be installed or cloned by itself; jump straight to the problem repo
you've been asked to start with.

---

## The problems

Work through these roughly in this order — they're arranged from
warm-up to hardest.

| # | Problem | Difficulty | What it's really testing |
|---|---|---|---|
| 1 | [Pair the Numbers](https://github.com/scottejames/pair-the-numbers-starter) | **Easiest** — warm-up | Hash map lookups, replacing an obvious-but-slow brute-force scan. A good confidence check that you can read a spec and structure clean code, nothing more. |
| 2 | [Split the Playlist](https://github.com/scottejames/split-the-playlist-starter) | **Easy** — warm-up | Binary search on the answer, paired with a greedy feasibility check. Still approachable, but the "obvious" back-of-envelope answer is subtly wrong. |
| 3 | [Escape the Vault](https://github.com/scottejames/escape-the-vault-starter) | **Hard** | Shortest-path search on a grid, complicated by keys and doors — a step up in state-tracking, not just pathfinding. |
| 4 | [Break the Cipher](https://github.com/scottejames/break-the-cipher-starter) | **Hard** | Dynamic programming over a string, with a real trap for anyone reaching for a greedy or brute-force-recursive shortcut. |
| 5 | [Bridge the Islands](https://github.com/scottejames/bridge-the-islands-starter) | **Hard** | Union-find (disjoint set union), including the path-compression / union-by-size details that matter once the input gets large. |

A couple of things worth knowing going in:

- **You don't need to already know the "textbook" technique for a
  problem.** Every problem is solvable by reasoning carefully from the
  spec and your own test results — the point is to see how you *get*
  there, not whether you memorised the right algorithm name in advance.
- **The first two are deliberately easier.** A clean pass there is a good
  sign, not a high bar — don't read too much into how fast you finish
  them. The real signal is in problems 3–5.
- Every problem repo is self-contained and has its own `README.md` with
  the actual problem statement, constraints, and a worked example, plus
  an `EXAMPLE.md` with a slower, step-by-step walkthrough. Start there.

---

## How to attack a problem

Once you've cloned a problem's starter repo (see below for how), here's a
sensible way to work through it:

1. **Read the whole `README.md` first**, all the way through, before
   writing any code — the problem statement, the worked example, and
   especially the `### Constraints` section. The size limits there
   usually contain a hint about what kind of approach is expected to
   scale.
2. **Read `EXAMPLE.md`.** It stages the same problem out by hand, one
   decision at a time, and is there specifically to make sure the
   *rules* of the problem are unambiguous before you commit to any
   approach.
3. **Skim `test_data/README.md`.** It documents every single test case
   and *why* it exists. If you get stuck on a failing case later, this
   is the fastest way to understand what it's actually checking.
4. **Only edit the one designated solution file** (named in the repo's
   own `README.md` — everything else is scaffolding that's already
   wired up for you: test data loading, the demo runner, the test
   harness, the shell scripts).
5. **Get something correct before you get it fast.** Aim to pass the
   `simple` tier first, then `medium`, then `hard`. It's completely fine
   to start with a straightforward approach and improve it once it's
   passing — that's a normal, visible part of the process, not something
   to hide.
6. **Run the test script constantly.** It's your entire feedback loop —
   there's no separate grading step or hidden test suite. Re-run it
   after every meaningful change.
7. **Take the `hard` tier seriously.** If it's slow, or a run just hangs
   and never finishes, that's real information about your approach, not
   bad luck — go back and re-read the constraints. Every problem is
   sized so a well-chosen approach finishes quickly and a naive one
   visibly struggles.
8. **You're done with a problem when the test script prints
   `TOTAL: <n> passed, 0 failed`, ending in `Efficiency band: Efficient`.**
   That exact line is what each repo's own README calls "Definition of
   done."

---

## Setting up your tools

You'll need **one** of Python or Java working from your terminal — pick
whichever you're more comfortable with, you don't need both. You'll also
need **Git**.

**If you already have Python, Java, and Git installed, you're all set —
skip straight to the next section.** Likewise, if you'd rather install
any of these a different way than described below (`pyenv`, `sdkman`,
`conda`, your Linux distro's package manager, WSL, whatever you're used
to), that's completely fine — the only actual requirement is that
`python3` (3.8+) or `java`/`javac` (a reasonably recent JDK, 11+) work
from a terminal, however you got there.

### macOS

The easiest path is [Homebrew](https://brew.sh), if you don't already
have it:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then, whichever you need:

```bash
brew install python      # for Python candidates
brew install openjdk     # for Java candidates
brew install git         # if you don't already have it
```

(`brew install openjdk` prints a short note at the end about linking the
JDK so `java`/`javac` are found on your PATH — follow whatever it tells
you to run.)

If you'd rather not use Homebrew, direct installers work just as well:
[python.org/downloads](https://www.python.org/downloads/) for Python, or
[adoptium.net](https://adoptium.net) (Eclipse Temurin) for a JDK. Git
usually comes preinstalled via the Xcode Command Line Tools — if
`git --version` doesn't work, running `git` for the first time will
offer to install them, or run `xcode-select --install` yourself.

### Windows

If you're on a reasonably modern Windows 10/11, `winget` (built in) is
the quickest route — open PowerShell and run whichever you need:

```powershell
winget install Python.Python.3.12
winget install EclipseAdoptium.Temurin.21.JDK
winget install Git.Git
```

Otherwise, direct installers work fine:
[python.org/downloads](https://www.python.org/downloads/) for Python
(**tick "Add python.exe to PATH"** during setup — it's easy to miss), or
[adoptium.net](https://adoptium.net) for a JDK. For Git, use
[git-scm.com/download/win](https://git-scm.com/download/win) — this also
installs **Git Bash**, which you'll want for the next bit.

**A Windows-specific note:** the `run.sh` / `test.sh` / `compile.sh`
scripts in each problem repo are bash scripts. On Windows, run them from
**Git Bash** (installed alongside Git for Windows above) rather than
Command Prompt or PowerShell, or use WSL if you already have it set up.
If you'd rather avoid both, each script is only a couple of lines —
open it in a text editor to see the plain `python3 ...` or
`javac`/`java ...` commands it runs, and just run those directly from
your normal prompt instead.

### Checking everything's working

From a terminal (or Git Bash, on Windows):

```bash
python3 --version   # 3.8 or higher
java -version        # a recent JDK — this also confirms javac is present
git --version
```

Any of these already working means you're good to go for that tool —
no need to reinstall anything.

---

## Getting your own copy, and pushing your solution

Each problem's starter repo is public, so you can clone it directly —
but you'll want your own repository to actually push your work to,
rather than pushing back into ours.

```bash
# 1. Clone the starter repo for the problem you're working on
git clone https://github.com/scottejames/pair-the-numbers-starter.git
cd pair-the-numbers-starter

# 2. Detach it from our repository, so there's no risk of pushing
#    your solution back to us, or of your solution living inside
#    our repo's history
git remote remove origin
```

Now create a fresh, empty repository under **your own** GitHub account.
We'd suggest making it **private**, so your solution isn't visible to
other candidates — but that's your call.

**If you have the GitHub CLI (`gh`) installed**, this is one command:

```bash
gh repo create my-pair-the-numbers-solution --private --source=. --remote=origin --push
```

**Otherwise**, create it on github.com first:

1. Go to [github.com/new](https://github.com/new), give it a name (e.g.
   `my-pair-the-numbers-solution`), set it to **Private**, and do
   **not** tick "Add a README" (your clone already has files in it).
2. Then, back in your terminal:

```bash
git remote add origin https://github.com/<your-username>/<your-repo-name>.git
git push -u origin master
```

From there, implement your solution in the one file the repo's `README.md`
points you at (e.g. `python/pair_numbers.py` or
`java/src/PairNumbers.java` — the exact name differs per problem), and
commit and push as you go, as often as you like:

```bash
git add .
git commit -m "Implement find_pair"
git push
```

Repeat the whole "clone, detach, create your own repo, push" flow for
each new problem you start.

---

## Using an editor

**Use whichever editor or IDE you're already comfortable with** — VS
Code, IntelliJ, PyCharm, Vim, whatever. None of this assumes a particular
tool. If you'd like a quick starting point with VS Code specifically:

1. Install [VS Code](https://code.visualstudio.com/) if you don't have
   it.
2. Open the folder you cloned: `File > Open Folder...`, or from a
   terminal already inside that folder, just run `code .`.
3. VS Code will likely prompt you to install a language extension the
   first time you open a `.py` or `.java` file — accept it (or install
   the **Python** extension, or the **Extension Pack for Java**,
   manually from the Extensions sidebar). This gets you syntax
   highlighting, autocomplete, and inline error checking.
4. Open your solution file from the Explorer sidebar on the left and
   start editing.
5. Use the built-in terminal (`` Terminal > New Terminal ``, or
   `` Ctrl+` ``/`` Cmd+` ``) to run `./scripts/test.sh` and friends right
   inside the editor — no need to switch windows.

That's genuinely optional — a plain text editor and a separate terminal
window works just as well.

---

Good luck! Start with [Pair the Numbers](https://github.com/scottejames/pair-the-numbers-starter)
if you're not sure where to begin.
