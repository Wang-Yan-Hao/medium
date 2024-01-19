# 我的 Git 指令小抄

## 注意事項
* commit 只要提交的話，很難刪掉，還沒提交 commit，很容易不見
* git 不要 add 大檔案和機密檔案
* git config 可以設定 alias
* 所有 HEAD, MASTER, origin ... 等關鍵字都只是一個指標

## 名詞

* working directory: 工作目錄
* stagin area(index): 暫存區
* repo: 儲存庫
* remtoe, origin: remote 指的是遠端的 repo，概念，origin 是真的一個指標指向一個 url
    ```
    $ git remote -v
    origin  https://github.com/example/repo.git (fetch)
    origin  https://github.com/example/repo.git (push)
    ```
* HEAD: 指向現在整個工作環境所在的 commit
* MASTER(任意 branch-name): branch 指標，現在 branch 最新所在的位置，所以切換 branch 就是把 HEAD 指標移動到 MASTER 指標上
* `add`: 把 working directory 的檔案加入到 staged region
* `commit`: 把 staged 的檔案加到 repo
* `reset`: 移動 master(branch pointer) 跟 HEAD，危險
* `checkout`: 移動 HEAD [細說git reset和git checkout的不同之處](https://medicineyeh.wordpress.com/2015/01/22/%E7%B4%B0%E8%AA%AAgit-reset%E5%92%8Cgit-checkout%E7%9A%84%E4%B8%8D%E5%90%8C%E4%B9%8B%E8%99%95/)
*  `revert`: 製造一個 commit 來 revert 之前 commit 動的一些檔案
*  `restore`: 復原檔案，不會動到指標，只動 working director [What is the `git restore` command and what is the difference between `git restore` and `git reset`?](https://stackoverflow.com/questions/58003030/what-is-the-git-restore-command-and-what-is-the-difference-between-git-restor)
*  `rebase`: 把一個 branch 以 ? commit 為基底，拔到另外一個以 ? commit 為基底的 branch 上。
    ![image](https://hackmd.io/_uploads/SJN2r3KOp.png) 來自 [Git 中文教學](https://www.youtube.com/playlist?list=PLlyOkSAh6TwcvJQ1UtvkSwhZWCaM_S07d) 投影片截圖


## Add and Commit

示意圖如下

![image](https://hackmd.io/_uploads/rkLfWEIKa.png) - [image source](https://www.earthdatascience.org/workshops/intro-version-control-git/basic-git-commands/)

```
git add -p # 在已經 track 的檔案
git checkout -p # 跟 add -p 相反, 不熟悉且危險

git commit --amend # 融合跟修改上一次 commit
```

## Restore

```
git restore <file> # work directory 的檔案修復到 HEAD (預設)
git restore --staged <file> # 讓已經進 staged 的檔案回到 work directory
git restore --source HEAD~2 <file> # 只修改一個檔案
# 以前沒有 git restore 都用 git checkout HEAD -- <filename>, 所以網路教學都教這個
```

## Reset
```
git reset [--soft | --mixed | --hard] [HEAD]
# soft 只是退回版本
# hard 退回版本並且將所有 commit 刪掉，更改文件的動作也刪掉
# --mixed 重製暫存區, 與上一次 commit 一樣
```

## Log
```
git log —oneline load.cpp # 只跟 load.cpp 有關的 commit
git log --name-only # 只顯示更改什麼檔案
```

## Diff

```
git diff # Working directory 跟 last commit 差異
git diff --staged # staged 跟 last commit 差異
git diff <commit>
git diff <commit> <commit>
```

## Branch and Checkout

```
git checkout <commit> # Move HEAD to the commit
git checkout <branch> # Move HEAD to the branch

git checkout -b <branch> # Create branch and checkout to that branch
```

## Branch

```
git branch -m <new-branch-name> # 改名
git branch -a # List branch include remote
git branch <nwe_branch> # Create branch

git branch -d <branch> # 刪除 branch
git branch -D <branch> # 無警告刪除 branch
```

## Merge

```
git merge <branch>
git merge <branch> --no-ff # merge 後會增加一個 commit 為 "merge ... branch"
```

## Rebase and Modify commit
* 不要 rebase 超過 branch base
* rebase 前要先做備份

```
git rebase <new base> # rebase current branch to new base, 自動調用共同的 commit
git rebse --onto <new base> <ref commit> <branch> # 把 ref commit 到 branch 之間的 commits 拔到 new base 上面
git rebase -i # 以現在自己為目標 往前幾個做 rebase
git rebase -i --root # 所有 commit rebase
```
![image](https://hackmd.io/_uploads/HksWP3Y_p.png)

## Remote and Github
```
git remote -v # 查看 remote url
git remote rename <a> <b> # 更改遠端 branch 名稱
git push <remote> <branch_1>:<branch_2> # 本地端 branch_1 遠端 branch_2
git push <remote> :<branch> # delete remote branch

git branch --set-upstream-to <remote-branch> # 設定 upstream branch
git branch --set-upstream-to=origin/develop develop
Branch 'develop' set up to track remote branch 'develop' from 'origin'.
git branch -vv # 查看現在 upstream 是誰
```

## Stash
```
git stash
git stash list
git stash pop stash@{n}
git stahs drop stash@{n}
```

## Patch and Cherry-Pick
...

## Reference

[Git 中文教學](https://www.youtube.com/playlist?list=PLlyOkSAh6TwcvJQ1UtvkSwhZWCaM_S07d)