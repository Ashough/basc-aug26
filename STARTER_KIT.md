# Claude Code Starter Kit — standing up the public repo

**This file is for you, not the public. Delete it before you push, or keep it —
your call, it does no harm.**

---

## Read this first

You are ten days from a talk. Learning a new tool is a fine idea; letting it
become a dependency for the talk is not.

**The fallback, which takes five minutes and needs no tooling at all:** go to
github.com → New repository → "uploading an existing file" → drag this whole
folder in → Commit. Done. Public repo, working link for your closing slide.

Do that **first**, today. Then learn Claude Code against a repo that already
exists and already works. If Claude Code frustrates you at 11pm on August 11,
you lose nothing.

Everything below assumes you've done that.

---

## Step 1 — Install

You have a Pro or Max account already, which is what Claude Code requires — <cite index="17-1">the free Claude.ai plan does not include Claude Code access</cite>.

**Option A — Desktop app (recommended for you).** <cite index="17-1">The Desktop app lets you use Claude Code without the terminal.</cite> Download it for macOS or Windows. Given that you're not a developer and the goal is to *learn the tool*, not to prove you can use a terminal, start here.

**Option B — Terminal.** <cite index="17-1">The native installer is the recommended method: on macOS, Linux, or WSL run `curl -fsSL https://claude.ai/install.sh | bash`; on Windows PowerShell run `irm https://claude.ai/install.ps1 | iex`.</cite>

Then check it worked:

```
claude --version
```

<cite index="17-1">A working installation prints a version number such as `2.1.211 (Claude Code)`.</cite> If anything looks wrong later, <cite index="17-1">`claude doctor` prints read-only installation and settings diagnostics without starting a session.</cite>

To start a session, <cite index="17-1">open a terminal in the project you want to work in and run `claude`</cite>. <cite index="17-1">Log in by following the browser prompts.</cite>

---

## Step 2 — Point it at this folder

Put this folder somewhere sensible (`~/Documents/owasp-demos` or similar), then
open Claude Code **in that folder**. This matters — Claude Code reads the
directory it's started in.

`CLAUDE.md` is already in the folder. Claude Code reads it automatically as
project instructions. It's the reason Claude Code won't "helpfully" refactor
your verified notebooks. **Do not delete it.**

---

## Step 3 — The prompts

Copy these one at a time. Wait for each to finish. Read what it says before
sending the next.

### Prompt 1 — Orientation

```
Read CLAUDE.md, then give me a one-paragraph summary of what this repo
is and what you are and aren't allowed to touch. Don't change anything yet.
```

*This is a test. If it doesn't mention that the notebooks are frozen, stop and
tell me — something's wrong with the setup.*

### Prompt 2 — Git, from zero

```
I've never used git. Walk me through initializing this folder as a git
repository and making a first commit. One step at a time: tell me what the
command does before you run it, run it, then confirm it worked. Don't run
more than one command before checking in with me.
```

### Prompt 3 — Push to GitHub

```
I have a GitHub account. Help me create a public repository and push this
to it. Ask me for anything you need from me rather than guessing. If a step
requires me to do something in a browser, tell me exactly what to click.
```

### Prompt 4 — Colab badges

```
The README has two "Open In Colab" badges with placeholder links (#).
Replace them with real Colab links pointing at the two notebooks in this
repo. Show me the URLs before you edit anything. Don't touch the notebooks.
```

### Prompt 5 — Verify

```
Check that both notebooks render correctly on github.com and that their
saved cell outputs are visible without running anything. Tell me if
anything is missing. Do not modify the notebooks.
```

### Prompt 6 — The one you should actually enjoy

```
Explain what just happened across all of those steps, as if to someone
who understands security architecture but has never used git. What is a
commit, what is a remote, and what did I actually do to GitHub?
```

---

## Step 4 — Fill in the placeholders yourself

The README has three `(#)` placeholders: your Substack, the SAIEF link, and the
two Colab badges. Prompt 4 handles the badges. Do the other two by hand — it's
faster than explaining them.

---

## When to stop and walk away

Claude Code is genuinely good and this is a reasonable first project. But:

- **If git authentication fights you for more than 20 minutes, stop.** Use the
  browser upload. This is a known-annoying part of git and it has nothing to do
  with your talk.
- **If Claude Code ever proposes touching a notebook, say no.** Then check
  `git status` and confirm nothing changed. `CLAUDE.md` should prevent this, but
  verify rather than trust.
- **After August 12, break it however you like.** Before August 12, the repo
  needs to be boring and working.

## The single check that protects you

Before the talk, from the repo folder:

```
git status
```

If it says anything other than a clean working tree, something changed that you
didn't intend. And open both notebooks on github.com one final time to confirm
the outputs are visible — that's the thing the audience will actually click.
