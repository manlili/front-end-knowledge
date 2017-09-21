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

## 描述从输入url到得到html的过程
### 加载资源的形式
- 输入url加载html页面
- 加载静态资源,img,css,字体文件等
- 加载脚本 `<script src="***"></script>`
### 上述的加载都符合一个过程
- 浏览器根据DNS服务器得到域名的IP地址
- 然后浏览器向这个IP地址的机器发送http或者https请求
- 服务器收到、处理并返回http请求
- 浏览器得到返回的内容

## 浏览器渲染页面的过程
- 根据HTML结构生成DOM Tree
- 根据CSS生成CSSOM
- 将DOM和CSSOM整合形成RenderTree
- 根据RenderTree开始渲染和展示页面
- 遇见`<script>`时，会执行JS并阻塞渲染，等js执行完页面继续渲染
### 浏览器渲染页面的实例
```bash
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<p>测试</p>
	</body>
</html>
```
上面按顺序执行

```bash
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="test.css"/>  <!--test.css内容涉及p标签样式-->
	</head>
	<body>
		<p>测试</p>
	</body>
</html>
```
上面渲染流程是
- 从上往下执行
- 遇见link链接的css,先去拿css样式
- 继续执行遇见body里面的P标签，由于css里面有P标签的样式，所以直接渲染P标签和它的样式
- 继续执行到完毕

```bash
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<p>测试</p>
		<script type="text/javascript">
			//涉及修改p标签的内容
		</script>
		<div>哈哈</div>
	</body>
</html>
```
上面渲染流程是
- 从上往下执行
- 继续执行遇见body里面的script，这时候停止渲染，直接去执行js内容，这时候发现P标签被修改，再去修改P标签，然后再去执行`<div>哈哈</div>`
- 继续执行到完毕

```bash
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<p>测试</p>
		<img src="***" alt="" />
		<div>哈哈</div>
	</body>
</html>
```
上面渲染流程是
- 从上往下执行
- 继续执行遇见body里面的img,由于img是异步加载的，继续执行`<div>哈哈</div>`，等图片加载完在插入html
- 继续执行到完毕

## 为什么要将css放到head中
因为在header中遇见css，直接去渲染css，等css渲染完再去渲染body里面的内容，body里面的内容可以直接渲染div和div的样式

### 为什么要把js放到body最下面
- 不会阻塞body里面的代码，更快的渲染页面
- 因为js脚本很有可能修改body里面html内容，所以最后执行完js，一次性修改html

## window.onload和DOMContentLoaded区别
### window.onload
页面所有的资源全部加载完才可以，包括图片，视频，字体等异步资源加载
### DOMContentLoaded
只需要DOM加载完便可，此时的图片，视频或者字体等异步资源可能还没加载完

## 页面性能优化

## 怎么保证程序的安全性
