<p align="center">
  <img src="logo.svg" alt="Coding Assessment" width="480">
</p>

# Working locally

This is the **install-it-yourself option** — if you'd rather not
install anything and just work in your browser instead, see
[CODESPACES.md](CODESPACES.md).

## Tools you'll need

**One** of Python or Java (your choice, you don't need both), plus
**Git**.

**If you already have these installed, skip straight to "Getting your
own copy" below.** Likewise, if you'd rather install any of these a
different way than described here (`pyenv`, `sdkman`, `conda`, your OS
package manager, WSL, whatever you're used to), that's completely
fine — the only actual requirement is that `python3` (3.8+) or
`java`/`javac` (a reasonably recent JDK, 11+) work from a terminal,
however you got there.

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
