# The Freedom to Fork

This is the slideshow for the "Freedom to Fork" demo talk at Software Freedom Day

The deck (`freedom-to-fork.md`) is itself the live demo: it gets forked, fixed, and merged back on stage.

## What it covers

- Why open source collaboration between strangers works (software and hardware)
- Licenses as the permission slip: MIT, GPL, Creative Commons
- Quick overview of other common licenses (Apache 2.0, BSD, LGPL, AGPL, MPL 2.0)
- How git works: commits as snapshots, history as safety
- Where people actually share repos (forges)
- GitHub vs. GitLab vs. Forgejo — ownership, licensing, self-hosting
- Instance admin vs. repo owner as distinct roles
- A live, on-stage fork → fix → PR → merge of this very deck

**Do not commit directly to `main`.** Fork this repo and open a pull request instead — that's the whole point.

## Viewing and presenting the slides

This deck is written for [Marp](https://marp.app), so you need something that understands Marp's frontmatter and `---` slide breaks to render it properly.

### Option 1: Kate + Marp CLI (recommended for Software Freedom Day - all FOSS)

**Editing:**
- Open `freedom-to-fork.md` in Kate
- Enable Markdown preview: View → Tool Views → Markdown Preview (or F7)
- Note: The preview shows Markdown content but not slide breaks

**Presenting:**
```bash
# Export to HTML slides (requires Node.js/npx)
npx @marp-team/marp-cli freedom-to-fork.md -o slides.html

# Open in browser and press F11 for fullscreen
firefox slides.html  # or your preferred browser
```

The exported HTML has built-in keyboard navigation (arrow keys, space, page-down/up).

**Git operations in Kate (for live demo - more accessible for newcomers):**
1. **Open the project**: File → Open Folder → select the cloned repo directory
2. **View git status**: Click the git sidebar icon (branch symbol on left toolbar)
   - Shows "Staged" and "Unstaged" files
3. **Commit**:
   - Click "Commit" button at top of git sidebar
   - A "Commit Changes" dialog opens
   - Enter commit message in the top field
   - Click "Commit" button
4. **Push**: Click "Push" button in git sidebar
5. **Pull**: Click "Pull" button in git sidebar

Note: For cloning, use command line first: `git clone https://forgejo.jaxlinux.com/demo-user/freedom-to-fork.git`, then open the folder in Kate.

### Option 2: VS Code + Marp extension (proprietary, but convenient)

**Editing & Presenting:**
- Install the "Marp for VS Code" extension
- Open `freedom-to-fork.md` and click the preview icon
- For presenting, still export to HTML as above (VS Code's preview isn't fullscreen)

**Git operations in VS Code (for live demo - more accessible for newcomers):**
1. **Clone**: Command Palette (Ctrl+Shift+P) → "Git: Clone"
   - Enter URL: `https://forgejo.jaxlinux.com/demo-user/freedom-to-fork.git`
2. **Commit**: Source Control sidebar (Ctrl+Shift+G)
   - Stage files with `+` button, enter message, click ✓ Commit
3. **Push**: Source Control sidebar → `...` menu → Push
4. **Pull**: Source Control sidebar → `...` menu → Pull

### Option 3: Command-line only (fastest, but may intimidate newcomers)

See the command examples in the slide deck itself.

## Git credentials setup (for live demo)

To clone repos without embedding credentials in URLs (i.e., simply `git clone https://forgejo.jaxlinux.com/rawdust/freedom-to-fork.git` or the demo-user fork URL), store credentials in git's credential helper before the presentation:

```bash
# Store rawdust credentials
git credential approve <<EOF
protocol=https
host=forgejo.jaxlinux.com
username=rawdust
password=<rawdust-password>
EOF

# Store demo-user credentials
git credential approve <<EOF
protocol=https
host=forgejo.jaxlinux.com
username=demo-user
password=<demo-user-password>
EOF
```

Now you can clone without putting passwords in the URL:
```bash
git clone https://forgejo.jaxlinux.com/rawdust/freedom-to-fork.git
git clone https://forgejo.jaxlinux.com/demo-user/freedom-to-fork.git
```

**After the presentation**, remove these credentials:

```bash
# Remove rawdust credentials
git credential reject <<EOF
protocol=https
host=forgejo.jaxlinux.com
username=rawdust
EOF

# Remove demo-user credentials
git credential reject <<EOF
protocol=https
host=forgejo.jaxlinux.com
username=demo-user
EOF
```

## Resetting between runs (rawdust only)

Before each rehearsal or the real talk, `main` needs to be back to a single commit with the planted GitLab-licensing error in place, so the live fork/fix/PR/merge demo has something to actually catch and fix. Run this as `rawdust`, in a local clone that has the just-merged fix pulled in:

```bash
git fetch origin
git switch main
git pull

# manually edit freedom-to-fork.md: in the "Meet the forges" table, change the GitLab cell back from "MIT (CE) / Proprietary (EE)" to "Proprietary"

git checkout --orphan squash-tmp
git add -A
git commit -m "Initial commit: Freedom to Fork slide deck"
git branch -M squash-tmp main
git push --force origin main
```

This collapses everything back into one clean root commit carrying the planted error, exactly like the repo's very first commit. Separately, delete `demo-user`'s fork (as `demo-user`: open the fork → Settings → Delete Repository) so the next run starts from a fresh fork with no stray branches. Old merged pull requests are harmless to leave in place — Forgejo has no way to delete a merged PR, so each new run just opens the next PR number.
