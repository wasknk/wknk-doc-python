# Git

## If remote repo has been renemed 
```bash
git remote -v
git remote set-url origin https://github.com/wasknk/wknk-doc-python.git
git remote -v
```


## Git push amend
```
git add -A
git commit --amend
git push --with-limit-lease
```

## Git first pushes the branch and sets the upstream relationship to dev
```
git branch dev
git switch dev
...
...
git push -u origin dev
```

## A Fix for an Accidental Commit and Push to Main

```
# 0. Get the commit hash of the last commit 
#    in main branch and copy the commit hash
git log -1

# 1. Go to the target branch and apply the commit
git switch dev
git cherry-pick <commit-hash>
git push origin dev

# 2. Correct the main branch history
git switch main
git reset --hard HEAD~1

# 3. Overwrite the remote main branch (DANGEROUS STEP)
git push --force-with-lease origin main
```

## git fetch and set remote 
```
git remote add upstream https://github.com/xxx/xxxxx.git
git remote -v
git fetch --all
```

## git change remote
```
git remote set-url origin https://github.com/xxx/xxxxx.git
git remote set-url upstream https://github.com/xxx/xxxxx.git
git remote -v
```

## git rebase
```
git rebase upstream/main

```

## git reset to last commit (have not push to remote)
```
git reset --mixed HEAD~1
```

## git gui
```
git-gui
```


## git checkout another branch dir 

```
# first make sure it is clear 
git branch 
git status
# than 
git checkout feat/another-branch -- scripts/
```

note: be careful , cause it will Overwrite the local scripts/ dir and its files 


## 

```
git stash	仅存储：已修改的旧文件 (Modified) 和已暂存的文件 (Staged)。	忽略：新创建的文件 (Untracked) 和 .gitignore 中的文件。
git stash -u	全部存储：包含已修改的旧文件、已暂存的文件，以及新创建的文件 (Untracked)。	忽略：仅忽略 .gitignore 中的文件。
git stash -a   全部存储，包括 .gitignore 中的要被忽略的文件

git stash list	查看储物柜里所有存着的内容。
git stash apply	应用改动，但不删除储物柜里的记录（比 pop 更安全）。
git stash drop	手动删除储物柜里最近的一条记录。
git stash clear	清空储物柜里的所有内容。
git stash -u	注意！ 默认 stash 不包含新创建的文件（untracked），加 -u 才能存。
```