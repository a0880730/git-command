# 常用git指令

- 查看git推送紀錄  
`git log`
- 查看目前 Git 變更狀態  
`git status`

# 基本指令
- 初始化 Git  
`git init`
- 儲存目前所有變更
`git add .`
- 提交一個紀錄
`git commit -m '首次提交'`
- 拉取一個遠端repo，**terminal記得停留在要存放的資料夾**
`git clone 遠端repo網址`
- 推送到遠端repo
`git push`
- 拉取遠端repo
`git pull`

# 分支
- 查看所有分支  
`git branch`
- 新建分支  
`git branch 新分支名稱`
- 切換分支  
`git checkout 分支名稱`
- 新增分支並且直接切換  
`git checkout -b 分支名稱`
- 移除分支  
`git branch -D 分支名稱`
- 在本地建立分支，並且推送到遠端
`git push -u origin 分支名稱`
- 刪除遠端分支
`git push origin --delete 分支名稱`

# 採櫻桃
當git其中一個紀錄是垃圾紀錄，可以使用採櫻桃的方式略過垃圾紀錄
1. 先查看log看要回朔到哪個版本  
`git log`
2. 回朔到該版本 **hash** 需從log取得  
`git reset --hard hash`
3. 跳過垃圾紀錄，逐一把後續的**hash**採集，一定要照順序!  
`git cherry-pick hash`
4. 採集完成查看log是否已經移除垃圾紀錄  
`git log`

# 回朔操作過程
1. 查看git操作紀錄，每個操作紀錄都有自己的**hash**  
`git reflog`
2. 回朔到某個操作紀錄，**hash**從reflog取得  
`git reset hash`
3. 因為上面 reset 指令沒有下 `--hard` 所以過程會保留，使用下方指令可清除所有過程  
`git checkout .`
4. 完成


# 暫時存檔
不想commit，但是又想切換分支或者先做別的功能時，可以使用stash
- 紀錄暫存  
`git stash save '暫存訊息'`
- 查看stash紀錄  
`git stash list`
- 取出stash紀錄  
`git stash pop`
- 取出stash紀錄，但是不要刪除stash紀錄，`index`帶入stash list的index  
`git stash apply index`
- 刪除stash紀錄  
`git stash drop`

# 將該紀錄撤銷，並且保留提交紀錄
- 查看log，找到要撤銷的時間點的**hash**
`git log`
- 撤銷該紀錄，**hash**從log取得
`git revert hash`
- 重新提交
`git push`