## Git & GitHub 

 * git init, clone, add, commit, push, pull  – basic workflow to create repos, track changes, and sync with remotes.
 * Branching: branch, checkout/switch, merge – isolate work, switch contexts, and combine changes.
 * Pull Requests & code review flow – propose changes from a branch and get them reviewed/merged on GitHub.
 * Resolving merge conflicts – manually fix overlapping changes when Git can’t auto-merge.
 * GitHub basics: repos, issues, PRs, branch protection – manage code, track work, review changes, and enforce rules.

### Version Control System

* Enables sharing of the code
* Enables Versioning

#### Versioning

#### Commands

origin = default name for remote repo you cloned from or added.  
upstream (-u) = tracks which remote branch your local branch pushes to / pulls from by default.

* `git --version` – show installed Git version.
* `git help <command>` – open help/manual for a specific Git command.
* `git config --global user.name` – show globally configured Git username.
* `git config --global user.email` – show globally configured Git email.
* `git config --global user.name Tulasi` – set global Git username to “Tulasi”.
* `git config --global user.email tulasi@gmail.com` – set global Git email.
* `git config --global init.defaultBranch` – show default branch name for new repos.
* `git config --global init.defaultBranch main` – set default branch name for new repos to `main`.
* `git config --list` – list all current Git configuration values.
* `git init` – create a new empty Git repository in the current folder.
* `git status` – show current branch and state of tracked/untracked/staged files.
* `git add file_name1 file_name2` – stage specific files for the next commit.
* `git add .` – stage all modified and new files in the current directory.
* `git commit -m "commit message"` – create a new snapshot (commit) with a message.
* `git commit --amend` – modify the last commit (message and/or staged content).
* `git show commit_id` – show details (diff + metadata) for a specific commit.
* `git log` – show full commit history for the current branch.
* `git log -n 5` – show the last 5 commits.
* `git log --oneline` – show compact one-line-per-commit history.
* `git log --oneline --graph --all` – compact ASCII graph of all branches and commits.
* `git pull` – fetch from the tracked remote branch and merge/rebase into current branch.
* `git push` – push your current branch’s commits to its tracked remote branch.
* `git diff` – show unstaged changes in working directory vs last commit.
* `git diff --cached` – show staged changes vs last commit.
* `git branch` – list local branches (and mark the current one).
* `git branch -M main` – rename current branch to `main` (force move).
* `git branch -d branch_name` – safely delete a local branch (if already merged).
* `git branch -D branch_name` – force delete a local branch (even if not merged).
* `git switch branch_name` – switch to an existing branch.
* `git switch -c branch_name` – create a new branch and switch to it.
* `git merge branch_name` – merge the named branch into your current branch.
* `git remote add origin github_repo_url` – add a remote named `origin` pointing to the given URL.
* `git remote -v` – list remotes and their fetch/push URLs.
* `git push origin local_branch_name` – push local branch to the remote `origin` under the same name.
* `git push -u origin local_branch_name` – push and set upstream so future `git push/pull` can omit args.
* `git clone git_hub_repo_url` – download a remote repo and set up `origin` automatically.
* `git pull` – (again) fetch + merge/rebase from the upstream tracking branch into current branch.
* `git pull origin main` – explicitly pull from `origin/main` into your current branch.
* `git pull --rebase origin master --allow-unrelated-histories` – pull from `origin/master`, rebasing your local commits on top, even if histories started separately.
* `git push --force-with-lease origin master` – force-push local `master` to remote but only if remote hasn’t changed unexpectedly (safer than `--force`).
* `git fetch` – download new commits/tags from remotes without merging them.
* `git restore file_name` – discard local changes in a file, resetting it to the last commit.
* `git restore --staged file_name` – unstage a file while keeping its changes in working directory.
* `git reset --soft HEAD~1` – move HEAD back one commit but keep all changes staged.
* `git reset --hard HEAD~1` – move HEAD back one commit and discard all associated changes.
* `git reset HEAD~1` – move HEAD back one commit and keep changes as unstaged in working directory.
* `git revert commit_id` – create a new commit that undoes the changes from a specific commit (safe for shared branches).
* `git reflog` – show history of where HEAD and branches have pointed (great for recovery after mistakes).
* `git stash push -m "comments"` – save current uncommitted changes to a stash with a message and clean working directory.
* `git stash list` – list all saved stashes.
* `git stash pop` – apply latest stash and remove it from the stash list.
* `git stash apply stash_id` – apply a specific stash without deleting it.
* `git stash drop stash_id` – delete a specific stash entry.
* `git rebase branch_name` – replay current branch’s commits on top of the given branch (rewrite base).
* `git rebase --continue` – continue an in-progress rebase after resolving conflicts.
* `git rebase --abort` – cancel the rebase and return to the state before it started.
* `git rebase --skip` – skip applying the current commit during a rebase.
* `git tag -a v1.0.0 -m "comments related to tag"` – create an annotated tag `v1.0.0` with a message at the current commit.
* `git tag v1.0.0` – create a lightweight tag `v1.0.0` pointing to the current commit.
* `git push origin v1.0.0` – push a specific tag to the remote.
* `git push origin --tags` – push all local tags to the remote.
* `git fetch origin --tags` – fetch all tags from the `origin` remote.
