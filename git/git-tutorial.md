**Git commands :**

- ```git init``` : For initializing any directory with git in it
- ```git clone repo-url``` : For cloning a repo
- ```git pull origin branchname``` : Pull latest change from remote repo
- ```git fetch``` : Directly fetch remote changes
- ```git push origin branchname``` : Pushing latest change to remote repo
</br></br>
- ```git diff``` : Show changes between commits
  - ```git diff filename``` : For a Filename
  - ```git diff HEAD``` : From last commit
  - ```git diff HEAD filename``` : From last commit, for a specific file
  - ```git diff --staged HEAD``` : From staging area
  - ```git diff --staged HEAD filename``` : From staging area but for a specific file
  - ```git diff firstCommitID secondCommitID``` : Between 2 commits
  - ```git diff HEAD HEAD^``` : Between last commit and HEAD
</br></br>
- ```git add .``` : For adding any directory and file(s)
- ```git commit -m 'random message'``` : For committing any file(s)
  - ```git commit -am 'amending commit'``` : For amending previous commit!
  </br>
- ```git stash``` : Git stash is used to save your uncommit changes so that you can work on something else and revert them from your working directory
  - ```git stash``` : For saving in stash
  - ```git stash list``` : For listing all stash history
  - ```git stash apply``` : For applying stash (then git add > git commit > git push )
  - ```git stash drop``` : For dropping stash changes
  - ```git stash -u``` : For stashing untrack file
  - ```git stash -a``` : For stashing all file
  - ```git stash pop``` : For only dropping last stash
</br>
</br>
- ```git revert``` :
  - ```git revert HEAD filename``` : For reverting commit for a particular file
  - ```git revert HEAD~``` : For any recent commit changes
- ```git log``` : Checking previous commits logs etc
  - ```git log --all --oneline --decorate --graph``` : For getting graph of git history
  - ```git log -- filename``` : For checking git history of a file
</br></br>
- ```git status``` : Check current status for git
- ```git mv filename new-filename``` : For moving a git added file.. without : mv and git add
- ```git rm filename``` : For deleting any file already in git
</br></br>
- ```git branch branchname``` : For creating a branch
  - ```git branch -a``` : List all git branches
  - ```git branch -m oldBranchName newBranchName``` : For renaming a branch
  - ```git branch -d branchname``` : For deleting a branch (PS : switch branch before deletion)
- ```git checkout branchname``` : For changing to a different branch
  - ```git checkout -b branchname``` : To create a new branch and switch to it in 1-go
- ```git merge branchname``` : For merging 2 branches together.. execute when in feature branch
  - ```git merge branchname -m 'Merging develop with master'``` : Auto merge (All commits will show on master/main)
- ```git rebase master``` : Similar to git merge (used for merging 2 branches).. it moves entire feature branch to begin on the tip of the master branch.. it rebase re-writes the project history y creating brand new commits for each commit in the original branch.
</br></br>**Advantage** : Much cleaner project history as it eliminates the unnecessary merge commits required by git merge and Rebasing also results in a perfectly linear project history
</br></br>
  - **Walk-through** : ```git checkout feature_branch``` and  ```git rebase master```
  - ```git rebase --continue``` and ```git rebase --abort``` and ```git rebase --skip```
  - ```git pull --rebase origin master``` : Rebase remote repo
</br></br>

- ```git show commitID``` : Checking commit info
- ```git config``` : For changing configuration for git bash
  - ```git config --global user.name 'Devang tomar'``` : For configuring username
  - ```git config --global user.email 'devangtomar123@gmail.com'``` : For configuring email
  - ```git config --global alias.someCommand "log --all -graph --decorate --oneline"``` : Now if you execute ```git someCommand``` will run ```git log --all -graph --decorate --oneline```
</br></br>
- ```git tag tagName``` : Tas are reference that point to specific points in git history. Tagging is generally used to capture a point in history that is used for a marked version release (eg., v1.1.0)
    - ```git tag --list``` : For listing all tags
    - ```git tag --delete tagName``` : For deleting specific tag
