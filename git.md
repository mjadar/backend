## GITHUB

it is a hosting platform where you can collaborate with oters on your repository

# What is GIT

- git is open source and free source control management (SCM)
- you can manage changes to file over time

## initial configuration

- configure name `git config --global user.name "mohamed jadar" `
- configure email address `git config --global user.email "mohamed.jadar@outlook.com`
- configure main branch `git config --global init.default branch main`

## Commands

- `git restore <file_name>` // to discard changes in working directory

- `git log` // to see commit history
- `git log --oneline` // commit history in oneline
- `git log -p` // detailed commit history with all changes

- `git commit -a -m "change xx" --amend` // will update last commit name

- `git reset COMMIT_ID` // jump to an old commit

- `git branch BRANCH_NAME` //to create a new branch
- `git branch -d BRANCH_TO_DELETE` //to delete a branch

- `git switch BRANCH_NAME` // to switch to a new branch
- `git switch -c BRANCH_NAME` // to create and switch to a new branch

```
# MERGE 2 BRANCHES
git switch main
git merge -m "merge fix" BRANCH_TO_BRING
git branch -d BRANCH_TO_DELETE
```

```
# MERGE CONFLICT
1- a new branch is created MAIN|MERGECONFLICT
2- update the file where there is a conflict
3- git commit -a -m "message"
then automatically you are switched to the main branch
```

- `git push -u origin main`
- `git push --all`

- `git pull = git fetch + git merge`

```
# SQUASH LAST 3 COMMITS
1- git rebase -i HEAD~3
2- change last 2 commit keyword to squash instead of pick
3- esc :wq
4- another file is popup, then comment out the last 2 comment names
```

```
# REBASE
1- git pull // master
2- git switch -c NEW_BRANCH
3- make updates
4- git checkout master
5- git pull // master to bring updated changes into master
6- git checkout NEW_BRANCH
7- git rebase master // re-anchor new_branch against latest changes
8-git checkout master
9- git rebase NEW_BRANCH
10- git push
```
