# Git & GitHub learning Roadmap — AI-Tutor Edition (g&glrate)

Built for pasting into a fresh Claude or ChatGPT session, one section at a time.
Inspired by Coddy's structure (bite-sized lessons → hands-on command practice → real project), but reshaped so an AI chat can run it as live tutoring instead of an in-browser terminal.

***

## HOW TO USE THIS

1. Paste the **Master Instruction** block below at the start of *every new session* (it tells the AI how to teach you).
2. Right after it, in the same message, paste **one Section** from this roadmap.
3. Actually run the commands in a real terminal (or GitHub's own repo) as you go — don't just read. Tell the AI what happened, especially when something breaks. Debugging a real error teaches more than any explanation.
4. Don't move to the next section until you can do its "Prove it" task without looking anything up.

***

## MASTER INSTRUCTION (paste this every time, unchanged)

```
You are my Git & GitHub tutor. I'm a complete beginner learning fast but
I want REAL understanding, not just commands to memorize.

Teach this section like an experienced senior dev mentoring me 1:1:
1. Explain the underlying MODEL first (what Git is actually doing internally —
   snapshots, the staging area, pointers, etc.) before giving commands.
   I should understand WHY a command works, not just what to type.
2. Use a simple everyday analogy for any new concept.
3. Give me the commands with a short real example for each.
4. Then give me a hands-on exercise I do myself in my own terminal —
   don't do it for me. Wait for me to report back what happened.
5. If I paste an error or unexpected output, diagnose it with me instead
   of just fixing it — ask what I think went wrong first.
6. End the section with 3-5 quiz questions to check real understanding
   (not just recall) and a "prove it" mini-task.
7. Keep explanations tight — no filler, no over-long preamble.
8. For any multiple-choice question, format it as an indented block with
   the options, and show the correct answer clearly after the options.

Here is the section we're covering in this session:
[PASTE SECTION HERE]
```

***

## PHASE 0 — Mental Model & Setup

**Goal:** Understand what version control actually solves, and get Git installed and configured before touching commands.

- What problem Git solves (vs. "final_v2_FINAL.docx" style file chaos)
- Version control concept: snapshots, not diffs — how Git differs from "track changes"
- Install Git, set `user.name` / `user.email`
- What a "repository" is (the `.git` folder) — local vs. remote, repo vs. GitHub
- Terminal basics needed going forward: `cd`, `ls`/`dir`, `pwd`

**Prove it:** Install Git, configure your identity, and explain in your own words the difference between Git (the tool) and GitHub (the service).

***

## PHASE 1 — Local Git Basics (the core loop)

**Goal:** Master the everyday loop you'll use in every single project: track, stage, commit.

- `git init` — what actually gets created
- The three areas: working directory → staging area → repository (commit history)
- `git status`, `git add`, `git commit -m`
- `git log` (and `--oneline`) — reading history
- `git diff` — working dir vs. staged vs. last commit
- `.gitignore` — what it's for and how patterns work
- Writing a good commit message

**Prove it:** Create a small project folder, make 5 real commits with meaningful messages, and use `git log` + `git diff` to explain what changed between two of them.

***

## PHASE 2 — Undoing Things (the part beginners fear most)

**Goal:** Stop being afraid of Git — know how to safely undo mistakes at every stage.

- Unstaging a file (`git restore --staged`)
- Discarding working-directory changes (`git restore`)
- Amending the last commit (`git commit --amend`)
- `git reset` — soft vs. mixed vs. hard, and why hard is dangerous
- `git revert` vs `git reset` — undoing published history safely
- `git stash` — saving work-in-progress without committing

**Prove it:** Deliberately break something 3 different ways (bad staged file, bad commit message, uncommitted mess) and fix each with the right command — then explain why you picked that one over the alternatives.

***

## PHASE 3 — Branching & Merging

**Goal:** Understand branches as lightweight pointers, not "copies" — and resolve a merge conflict without panicking.

- What a branch actually is (a movable pointer, not a folder copy)
- `git branch`, `git switch` / `git checkout -b`
- Merging: fast-forward vs. three-way merge
- What causes a merge conflict and how Git marks it in a file
- Resolving a conflict by hand, then completing the merge
- When and why to delete branches after merging

**Prove it:** Create two branches that touch the same line of the same file, merge them, get a real conflict, and resolve it manually (no "accept theirs" shortcuts) — then explain what the conflict markers meant.

***

## PHASE 4 — Remotes & GitHub

**Goal:** Connect your local repo to GitHub and understand push/pull as syncing between independent histories, not "saving to the cloud."

- Creating a GitHub account/repo
- HTTPS vs SSH (and setting up an SSH key — worth doing early)
- `git clone` vs `git init` + `git remote add`
- `git push`, `git pull` vs `git fetch` (why fetch is the "safe" one)
- Tracking branches (`origin/main` vs `main`)
- Reading a repo's page on GitHub: commits, branches, file history

**Prove it:** Push a local repo to a new GitHub repo, make a commit locally, push it, then make a *different* change directly on GitHub and pull it down.

***

## PHASE 5 — Collaboration Workflow

**Goal:** Work the way real teams and open-source projects work.

- Forking vs. cloning — when each applies
- The Pull Request (PR) workflow end-to-end: branch → commit → push → open PR
- Writing a PR description that explains *why*, not just *what*
- Reviewing a diff, requesting/making changes
- Issues: linking commits/PRs to issues
- Basic GitHub flow vs. Git flow (just enough to recognize the terms)

**Prove it:** Open a PR on your own repo (branch → PR → merge) from start to finish, and, if you're ready, make one real contribution to a small open-source repo (even a typo fix in docs counts).

***

## PHASE 6 — Leveling Up (polish + the last 20%)

**Goal:** Fill the gaps that separate "knows Git" from "comfortable with Git."

- `git rebase` (basic, interactive) vs. merge — what it's for and its one big danger (rewriting shared history)
- Tags and releases
- A good README (and why it matters more than people think)
- `git blame`, `git show` for digging into history
- Cheat-sheet moment: build your own personal command reference from everything above, in your own words

**Prove it:** Rebase a feature branch onto an updated main, tag a release, and write a README for one of your practice repos.

***

## CAPSTONE

Pick one:
- Contribute a real PR to an open-source project (docs fix is a fine first one)
- Build a small personal project from scratch using the full workflow: branches for every feature, PRs even though you're solo, a clean commit history, and a proper README

Either way, walk the AI tutor through your process afterward and have it grill you on *why* you made each Git decision — that's the real test of whether this stuck.
