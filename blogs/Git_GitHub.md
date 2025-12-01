## Git & GitHub 

 * git init, clone, add, commit, push, pull
 * Branching: branch, checkout, merge
 * Pull Requests & code review flow
 * Resolving merge conflicts
 * GitHub basics: repos, issues, PRs, branch protection


### Version Control System

* Enables sharing of the code
* Enables Versioning

#### Versioning

#### Commands

origin = default name for remote you cloned from or added.
upstream (-u) = default remote branch linked to local branch.

* `git --version`
* `git help <command>`
* `git config --global user.name`
* `git config --global user.emial`
* `git config --global user.name Tulasi`
* `git config --global user.email tulasi@gmail.com`
* `git config --global init.defaultBranch`
* `git config --global init.defaultBranch main`
* `git config --list`
* `git init`
* `git status`
* `git add file_name1 file_name2`
* `git add .`
* `git commit -m "commit message"`
* `git commit --amend`
* `git show commit_id`
* `git log`
* `git log -n 5`
* `git log --oneline`
* `git log --oneline` --graph --all
* `git pull`
* `git push`
* `git diff`
* `git diff --cached`
* `git branch`
* `git branch -M main`
* `git branch -d branch_name`
* `git branch -D branch_name`
* `git switch branch_name`
* `git switch -c branch_name`
* `git merge branch_name`
* `git remote add origin github_repo_url`
* `git remote -v`
* `git push origin local_branch_name`
* `git push -u origin local_branch_name`
* `git clone git_hub_repo_url`
* `git pull`
* `git pull origin main`
* `git pull --rebase origin master --allow-unrelated-histories`
* `git push --force-with-lease origin master`
* `git fetch`
* `git restore file_name`
* `git restore --staged file_name`
* `git reset --soft HEAD~1`
* `git reset --hard HEAD~1`
* `git reset HEAD~1`
* `git revert commit_id`
* `git reflog`
* `git stash push -m "comments"`
* `git stash list`
* `git stash pop`
* `git stash apply stach_id`
* `git stash drop stach_id`
