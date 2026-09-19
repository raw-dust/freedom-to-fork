---
marp: true
theme: default
paginate: true
footer: 'The Freedom to Fork - Rajesh Verma'
---

<!-- PRESENTER NOTE: This file is the actual demo repo. It lives on the Forgejo instance under rawdust's account. demo-user will fork THIS repo, fix the planted error on the "Meet the forges" slide (GitLab listed as "Proprietary" instead of "MIT (CE) / Proprietary (EE)"), and PR it back. -->

# The Freedom to Fork
### Open Source Collaboration for Any Project


<!-- ~1 min: quick welcome, no need to over-explain the title yet -->

---

## Why does forking matter?

- Linux, Firefox, GIMP, LibreOffice — real software built by strangers, who mostly never met
- It's not just software — open source hardware works the same way: 3D-printable designs and open circuit board layouts get shared, tweaked, and shared again by people who've never spoken
- What makes all of that sharing possible: **the freedom to copy, change, and give back**


<!-- ~2 min. Sets the frame with real examples people recognize. Don't over-explain "fork" yet, that's later. Legality comes next slide — keep this one about sharing/collaboration, not licenses. -->

---

## Licenses: the permission slip

A license is what turns "here's some code" into "here's some code you're *allowed* to build on."

No license = **all rights reserved by default**, even on public GitHub repos.

<!-- ~1 min transition into the three core licenses -->

---

## MIT License

- Do almost anything: use, modify, sell, close-source it
- Only real requirement: keep the copyright notice
- The most common "permissive" license
- You've probably seen this in the "About" or "Open Source Licenses" screen of apps you use

<!-- ~1.5 min -->

---

## GPL (GNU General Public License)

- "Copyleft" — you can change it, but if you distribute your changes, they have to stay open under GPL too
- The freedom is designed to be **contagious**, on purpose


<!-- ~1.5 min -->

---

## Creative Commons

- For non-code creative work: docs, art, photos — and most 3D-printable designs you'll find on Thingiverse, Printables, etc.
- Several flavors: CC-BY (attribution only) up to CC-BY-NC-ND (attribution, no commercial use, no derivatives)
- Circuit board designs usually skip CC entirely for dedicated open hardware licenses (CERN OHL, TAPR OHL) instead

<!-- ~1.5 min -->

---

## There's a lot more out there

- **Apache 2.0** — permissive, adds an explicit patent grant
- **BSD (2/3-clause)** — MIT's close cousin
- **LGPL** — "weak copyleft," safe to link from proprietary code
- **AGPL** — closes the "I only run it as a SaaS" copyleft loophole
- **MPL 2.0** — file-level copyleft (this is Firefox's and Brave's license)

<!-- ~30 sec, fast, don't dwell -->

---

## Version control: git

- Git saves **snapshots** of your code as you work. Each one a safe checkpoint called a **commit**
- Make changes without fear of breaking anything: if something goes wrong, just go back to an earlier commit
- Every commit records exactly what changed and **why** so anyone else can see the full history
- Share that whole history, snapshots and all, by pushing it somewhere others can pull down

<!-- ~1.5 min. Bridges from "licenses grant permission" to "git is how that permission actually gets exercised." Plants the word "commit" now so the live demo's git commands later feel familiar. -->

---

## Where people actually share repos

- Git itself doesn't need a website — it's just a history of changes
- But hosting that history somewhere with issues, pull requests, and a UI is how most real collaboration happens
- GitHub, GitLab, Forgejo/Codeberg, sourcehut, or self-hosted
- Let's meet three of them

<!-- ~1 min. Sets up "Meet the forges" next. -->

---

## Meet the forges

| | GitHub | GitLab | Forgejo |
|---|---|---|---|
| Owner | Microsoft | GitLab Inc. | Non-profit community |
| License | Proprietary | Proprietary | GPLv3 |
| Self-hostable | No | Yes (paid) | Yes, free |

<!-- ⚠️ PLANTED ERROR — this is intentional. GitLab Community Edition is actually MIT-licensed / open source; only GitLab Enterprise Edition is proprietary (same "open core" pattern as Gitea/Forgejo). The row above overstates it as flatly "Proprietary." Friend catches this on the next beat — do NOT pre-empt it, let it land as written. -->

---

<!-- ~30 sec — no slide content, just the live moment -->

<!-- PRESENTER NOTE: this is where your friend calls out the GitLab row. Confirm out loud, don't be defensive about it: "You're right — GitLab CE is actually MIT-licensed and open source, only Enterprise Edition is proprietary. ...and that's actually a mistake sitting in this exact deck's source file. Let's go fix it — for real." -->

## wait somethin's wrong with these slides
- Let's fix that now LIVE

---

## This deck is a repo

- These slides are written in **Marp** — plain Markdown, MIT-licensed
- Markdown diffs cleanly in git, unlike a binary .pptx — that's *why* "slides as a repo" works at all
- The GitLab error we just found? It's a line in this file, in a repo, on our Forgejo instance, right now

<!-- ~1.5-2 min. This is the pivot into the live demo. -->

---

## Instance admin vs. repo owner

- **rawdust** is the admin of this Forgejo instance — controls the whole server
- **rawdust** also happens to own *this* repo — but that's a separate role, controls just this one project
- Any user could own a repo here, admin or not

<!-- ~1 min. Quick, don't overdo it — just prevents confusion later when rawdust does the merge. -->

---

## Let's go fix it: Fork

**Forking creates your own full copy of the repo:**

1. Visit https://forgejo.jaxlinux.com/rawdust/freedom-to-fork
2. Click the "Fork" button (top-right)
3. Choose destination: confirm "demo-user" as the owner
4. Click "Fork Repository" to create your copy

Now you have: `https://forgejo.jaxlinux.com/demo-user/freedom-to-fork`

<!-- ~2 min. Narrate what a fork actually is: your own full copy on the server, the original owner doesn't see or control it. -->

---

## Clone your fork locally

**Command line:**
```bash
git clone https://forgejo.jaxlinux.com/demo-user/freedom-to-fork.git
cd freedom-to-fork
```

**VS Code:**
- Source Control → Clone Repository
- Paste URL: `https://forgejo.jaxlinux.com/demo-user/freedom-to-fork.git`
- Choose folder location

<!-- ~1-2 min. -->

---

## While we're in here: a warning

**Command line:**
```bash
ls -la
# notice: secrets.txt.template, not secrets.txt
cat .gitignore
```

**VS Code:**
- Explorer sidebar: notice `secrets.txt.template` (not `secrets.txt`)
- Open `.gitignore` file

**Never commit API keys or credentials.** Once they're in git history, they're effectively public forever — even if you delete the file in a later commit.

<!-- ~30 sec. One line, then move on — this is a warning, not a demo. -->

---

## Fix + commit

**Command line:**
```bash
git switch -c fix-gitlab-license
# edit freedom-to-fork.md: in the "Meet the forges" table,
# change GitLab's License cell from "Proprietary" to "MIT (CE) / Proprietary (EE)"
git add freedom-to-fork.md
git commit -m "Fix GitLab licensing claim (CE is MIT, EE is proprietary)"
git push origin fix-gitlab-license
```

**VS Code:**
- Bottom-left: click "main" → Create new branch `fix-gitlab-license`
- Edit table: `Proprietary` → `MIT (CE) / Proprietary (EE)` → Save (Ctrl+S)
- Source Control → Stage (+) → Type message → Commit (✓)
- Click "Publish Branch" button that appears

<!-- ~3 min -->

---

## Open the pull request

- demo-user opens a PR on Forgejo: their branch → rawdust's main
- rawdust reviews the diff
- **demo-user cannot merge this PR** — only rawdust can, because rawdust owns the repo
- rawdust clicks merge

<!-- ~5-7 min live. This is the core "aha" payoff — slow down here. **Say this part out loud.** -->

---

## The payoff

**Command line (on rawdust's machine, in the ORIGINAL local clone):**
```bash
git pull
cat freedom-to-fork.md
# the GitLab line is now correct — live, in the actual deck
```

**VS Code (on rawdust's machine):**
- Source Control sidebar → `...` menu → Pull
- Open freedom-to-fork.md
- The GitLab line is now correct — live, in the actual deck

<!-- Make sure this terminal/tab or VS Code window is already open before the talk starts. Confirm the exact path during your dry run. -->

---

## Wrap-up

- None of this — forking, cloning, merging — happens without the license granting it on day one
- Same loop works identically on GitHub, GitLab, Forgejo, anywhere
- And the same freedom applies whether it's code, a 3D-printable design, or a PCB layout
- The platform doesn't grant the freedom. The license does.

---

# Thank you!

Questions?

Rajesh Verma
rv49er@gmail.com
