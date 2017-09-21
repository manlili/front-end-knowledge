# 前端相关问题
排序不分难易,答案仅供参考

## 平时开发中使用的IDE
- sublime
- webstorm
- atom

## 简述你们团队的协作工具，如何解决代码冲突？
一般是使用git或者svn
### 常见的git命令
```bash
//查看编辑的情况  
git status 

//提交到本地仓库  
git commit -m "提交的理由"

//提交到远程仓库  
git push

//获取最新代码    
git pull

//查看当前没有add过的文件修改的细节
git diff 文件路径

//撤销未提交到本地仓库的文件
git checkout 文件路径或者.

//查看已经add但没有commit的修改细节
git diff --cached 文件路径

//撤销已经add但没有commit的文件，注意是撤销为add前状态，并未销毁
git reset HEAD 文件路径名或者*

//撤销已commit但没有push的文件，注意是销毁全部修改的内容
git log 
git reset --hard 上一次的序列号

//删除某一次已经提交到远程仓库的提交
git log 
git reset --hard HEAD 上一次的序列号

//恢复某一次从线上仓库误删除的提交
git reflog
git reset --hard 序列号

//更新分支，尤其是远程分支
git fetch -p

//获取所有分支
git branch -a

//切出新分支
git checkout -b 分支名

//将本地分支推到远程分支
git push --set-upstream origin 本地分支名

//删除本地分支
git branch -D 分支名

//删除远程分支
git push origin :分支名

//merge
git merge 想要被融合的分支名

// 查找某句是谁修改的
git log -S "代码细节"
```
### 关于git如何解决代码冲突

## 上线和回滚的流程
### 上线流程
使用专门的发布工具完成，目前使用的是Jenkins,但是注意要点
- 开发前从master切出新分支，开发和测试
- 将需要发版的代码打包成需要版本后后缀的压缩包进行备份
- 发布完成后将代码合并到master,保持master永远是线上最新的代码
### 回滚流程
- 将线上出问题的代码打包压缩，备份
- 将上线前已经备份的压缩包解压，发布到服务器，并生成新的版本号

