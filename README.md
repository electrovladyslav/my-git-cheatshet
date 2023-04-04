# My Git cheatsheet
## Another git chetsheets
- Legendary (the only complete guide) Oh sh*t git https://ohshitgit.com/
- Git CheatSheet https://cs.fyi/guide/git-cheatsheet
- Advanced tips https://www.atlassian.com/git
- Codeacademy
    - Learn GitHub: Best Practices https://www.codecademy.com/learn/learn-github-best-practices
    - Deploying Websites using Git and GitHub https://www.codecademy.com/learn/deploying-websites-using-git-and-github
- Udemy Git: Become an Expert in Git & GitHub in 4 Hours (free) https://www.udemy.com/course/git-expert-4-hours/
- Git Fundamentals (A to Z) - 10 days free https://www.pluralsight.com/courses/git-fundamentals
- Version Control with Git (free) https://www.coursera.org/learn/version-control-with-git
- Interactive simulator of useful git comands - https://learngitbranching.js.org/


### Delete all branches locally except for master
```shell
git branch | grep -v "master" | xargs git branch -D
```

### View the commit history
```shell
git log --pretty=oneline --abbrev-commit --graph --decorate
git log --graph --oneline --decorate --all
```

## Cherry-pick
### To cherry-pick all the commits from commit A to commit B (where A is older than B), run:
```shell
git cherry-pick A^..B
```

### If you want to ignore "A" itself, run:
```shell
git cherry-pick A..B
```

### Use '-n' flag with the cherry-picking which is "no commit"
```shell
git cherry-pick -n <HASH>
```

## SSH
### Add key to ssh-agent, check its availability with:
```shell
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/github_rsa
ssh -T git@github.com
```

## Routine work
### Clone a remote repository to a local directory
```shell
git clone url folder_name
```

### Fetch all changes from the remote server
```shell
git fetch
```

### Pull changes from the remote branch that the local branch is tracking with
```shell
git pull
```

### With git pull --ff-only, Git will update your branch only if it can be “fast-forwarded” without creating new commits.
```shell
git pull --ff-only
```

### Checkout and track a remote branch
```shell
git checkout -b <branch-name> origin/<branch-name>
```

## Diff
### View changes between current uncommitted files and the last commit
```shell
git diff
```

### View changes between current added files and the last commit
```shell
git diff --cached
```

### Show differences between two branches
```shell
git diff <branch1> <branch2>
```

### Show only the names of files that differ between two branches
```shell
git diff --name-only <branch1> <branch2>
```

### Show a list of files that differ between two branches with their status (added/deleted/modified)
```shell
git diff --name-status <branch1> <branch2>
```

### Save the diff to a file
```shell
git diff > 20150203_someChanges.diff
git diff > some-changes.patch
```

### Apply changes from a diff file
```shell
git apply /path/to/some-changes.patch
```

### If there are errors related to whitespaces, apply the diff file using:
```shell
git apply --reject --whitespace=fix mychanges.patch
```
The --reject option will instruct git to not fail if it cannot determine
how to apply a patch, but instead to apply individual hunks it can apply
and create reject files (.rej) for hunks it cannot apply.
Additionally, --whitespace=fix will warn about whitespace errors and try to fix them,
rather than refusing to apply an otherwise applicable hunk.

## log

### Show the last 2 commits with messages
```shell
git log -2
```

### Show all changes to files
```shell
git log -f
```

### Show only file names
```shell
git log --name-only
```

### Switch HEAD to commit 332d568f3249db83baa0784f6f4738cf2842490c
```shell
git checkout 332d568f3249db83baa0784f6f4738cf2842490c
```

## remote
### Show a list of remote repositories
```shell
git remote -v
```

### Add the remote repository remote_repo_url with the name remote_repo
```shell
git remote add remote_repo remote_repo_url:
```

## push
### Publish changes from the local master branch to the remote_branch branch of the remote repository remote_repo. If the remote_branch branch does not exist, it will be created
```shell
git push remote_repo remote_branch
```

### Send the local serverfix branch to the awesomebranch branch of the remote project remote_repo
```shell
git push remote_repo serverfix:awesomebranch
```

### Push the dist sub-folder to the gh-pages branch
```shell
git subtree push --prefix dist origin gh-pages
```

## git branch
### Rename the current local branch local_branch
```shell
[local_branch] git branch -m <new_name>
```

### Rename the local branch old_name
```shell
[local_branch] git branch -m <old_name> <new_name>
```

### Delete the local branch testing
```shell
git branch -d testing
```

### Delete the remote branch testing in the remote repository origin
```shell
git push origin :testing
git push origin --delete testing
```

### List remote branches
```shell
git branch -r
git remote show origin
```

###List local and remote branches
```shell
git branch -a
```

### Undo changes to not added file
```shell
git checkout
git checkout [file]
```

### Create a new local branch new_loc_branch and switch to it
```shell
git checkout -b [new_loc_branch]
```

### Create a new local branch new_loc_branch, download the contents of the remote branch origin/rem_branch, and switch to it
```shell
git checkout origin/rem_branch -b new_loc_branch
```

## git merge
### Merge changes from local_branch_2 into local_branch_1
```shell
[local_branch_1] git merge local_branch_2
```

### Create a new remote branch, push changes to it, and link it to the current branch.
```shell
git push --set-upstream origin module3-task1
```

## git stash

### Hide changes and return to the last commit state
```
git stash
```

### Show a list of all hidden states
```shell
git stash list
```

### To see the files in a specific stash (0 is the latest, 1 is the penultimate, etc.)
```shell
git stash show stash@{2}
```

### To see the edits in these files, add -r
```shell
git stash show -p stash@{2}
```

### Retrieve changes from the latest hidden state and apply them to the current version
```shell
git stash apply
```

### Delete the latest changes in the list
```shell
git stash drop
```

### Equivalent to apply + drop
```shell
git stash pop
```

### Clear the list of changes
```shell
git stash clear
```

## git config
### set the Sublime as a default text editor
```shell
git config --global core.editor "'c:/program files/sublime text 3/subl.exe' -w"
```

### Set a global name of a git user
```shell
git config --global user.name "John Doe"
```

### Set a global email of a git user
```shell
git config --global user.email "send_me_letter@mail.com"
```


## git alias ([doc](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases))
### Change long `checkout` to `co`
```shell
 git config --global alias.co checkout
 ```
### Change long `status` to `st`
```shell
 git config --global alias.st status
 ```

### Show list of all configs
```shell
git config --list
```


## git amend
### Change the text of last commit to "Right text"
```shell
git commit --amend -m 'Right text'
```

```shell
git commit -a --amend
```

### Add some changes to the last commit without editing its comment
```shell
git commit --amend --no-edit
```
The resulting commit will replace the incomplete commit.
In this case, everything will be as if the changes in the file occurred in one commit.

## git reset

### Cancel adding README to the staged files for commit
```shell
$ git reset -- README
```

### This command will undo the last commit (but not the changes you made, they will still be saved).
```shell
git reset --soft HEAD^
```

### If the last commit is terrible, you can just remove it altogether:
```shell
git reset --hard HEAD^
```

### Remove commit from remote repo
All of this works if you haven't published your changes yet. 
If you have, then the only thing left to do is to make a commit that cancels some other commit:
```shell
git revert commit-sha1
git push
```

## git blame
### Check who and when changed file file-name
```shell
git blame file-name
```

 For example, suppose you look at git blame's output. Here -L 150,+11 means "only look at the lines 150 to 150+11"
```shell
git blame -L 150,+11 -- git-web--browse.sh
```

And you want to know the history of what is now line 155.
Then, use git log. Here, -L 155,155:git-web--browse.sh means "trace the evolution of lines 155 to 155 in the file named git-web--browse.sh".
```shell
git log --pretty=short -u -L 155,155:git-web--browse.sh
```

## git rm
### Remove application.yml from repo, but keep it on disk
```shell
git rm --cached --ignore-unmatch application.yml
```

```shell
git mv oldname newname
```
is just shorthand for:
```shell
mv oldname newname
git add newname
git rm oldname
```
i.e. it updates the index for both old and new paths automatically.

### push the branch to master with squashing all your commits to 1
To push my work to master on one of my previous places of work I had to do something like this
```
git stash
git fetch
git checkout master
git pull --ff-only
git checkout username/is15126
git checkout -b username/is15126b
git rebase master
git checkout master
git merge --squash username/is15126b
git commit -m "IS-15126: XXX"git push origin master
```
