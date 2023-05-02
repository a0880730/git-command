# 常用git指令

- 查看git提交紀錄  
`git log`
- 查看目前 Git 變更狀態  
`git status`

# 基本指令
- 初始化 Git  
`git init`
- 儲存目前所有變更  
`git add .`
- 提交一個紀錄  
`git commit -m '提交描述'`
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
- 將本地分支推送到遠端  
`git push -u origin 分支名稱`
- 查看遠端分支  
`git branch -r`
- 切換至遠端分支，此操作本地會同步出現該分支    
`git checkout 分支名稱`
- 刪除遠端分支  
`git push origin --delete 分支名稱`
- 同步遠端主線的紀錄到遠端分支，使用此方法所有提交紀錄會同步到分支  
`git pull origin main`


# 採櫻桃
當提交紀錄其中有錯誤或多餘的紀錄，可以使用採櫻桃的方式略過這些紀錄  
1. 先查看log看要回朔到哪個版本  
`git log`
2. 回朔到該版本， **hash** 需從log取得  
`git reset --hard hash`
3. 跳過多餘紀錄，逐一把後續的**hash**採集，一定要照順序!  
`git cherry-pick hash`
4. 採集完成查看log是否已經移除垃圾紀錄  
`git log`
5. 如果遠端已經有更新的版本，會出現錯誤，此時可以使用`-f`指令強制push，覆蓋之前的紀錄，或者再切出一個新的分支，新的分支就會是正確的提交紀錄
`git push -f`  
or
`git checkout -b 新分支名稱`

# 回朔操作
可以將檔案版本回朔至某次操作"之後"
1. 查看git操作紀錄，每個操作紀錄都有自己的**hash**  
`git reflog`
2. 回朔到某個操作紀錄，**hash**從reflog取得  
`git reset hash` 會保留過程  
`git reset --hard hash` 不會保留過程
3. 如果上面 reset 指令沒有下 `--hard` ，可使用此指令清除所有過程，或手動編輯  
`git checkout .`
4. 重新提交  
`git push`  
如果已經有更新的版本push上去，會出現錯誤，此時可以使用`-f`指令強制push  
`git push -f`


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


# 撤銷提交
可以將檔案版本切回到某個提交紀錄"之前"，意思是撤銷該次以及之後的所有提交，
git會建立一個新的commit，並且把這段時間的所有變更反向操作，因此所有提交紀錄都會保留。
1. 查看log，找到要撤銷的紀錄點**hash**  
`git log`
2. 撤銷該紀錄，**hash**從log取得  
`git revert hash`  
輸入後會進入vim，輸入`:x!`Enter後離開  
3. 重新提交  
`git push`


# 合併衝突的處理
1. 先使用 `git pull` 拉取遠端分支 
如果有看到 `hint: git config pull.rebase false; #merge` 的訊息，可以使用下方指令設定  
`hint: git config pull.rebase false`  
2. 成功執行 `git pull` 時，如果有衝突，會看到衝突的檔案視窗，修改成想要儲存的版本之後，儲存離開
3. 執行 `git add .`，將修改的檔案加入暫存
4. 執行 `git commit -m '衝突處理'`，提交衝突處理
5. 執行 `git push`，推送到遠端
