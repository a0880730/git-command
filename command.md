# 常用查看git狀態的指令
## 查看git推送紀錄
`git log`
## 查看目前git變更狀態
`git status`

# 執行紀錄
`git init`
`git add .`
`git commit -m '首次提交'`

# 分支
## 查看所有分支
`git branch`
## 新建分支
`git branch 新分支名稱`
## 切換分支
`git checkout 分支名稱`
## 新增分支並且直接切換過去
`git checkout -b 分支名稱`
## 移除分支
`git branch -D 分支名稱`

# 採櫻桃
## 當git其中一個紀錄是垃圾紀錄，可以使用採櫻桃的方式略過垃圾紀錄
### 先查看log看要回朔到哪個版本
`git log`
### 回朔到該版本 *hash* 需從log取得
`git reset --hard *hash*` 
### 跳過垃圾紀錄，逐一把後續的hash採集，一定要照順序!
`git cherry-pick *hash*`
### 採集完成查看log是否已經移除垃圾紀錄
`git log`

# 回朔操作過程
## 查看git操作紀錄，每個操作紀錄都有自己的hash
`git reflog`
## 回朔到某個操作紀錄，*hash*帶入reflog查到的hash
`git reset *hash*`
## 因為上面reset指令沒有下 `--hard` 所以過程會保留，使用下方指令可清除所有過程
`git checkout .`
## 完成
