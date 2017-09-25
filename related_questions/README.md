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

//merge mster提示Please enter a commit message to explain why this merge is necessary.
1.按键盘字母 i 进入insert模式

2.修改最上面那行黄色合并信息,可以不修改

3.按键盘左上角"Esc"

4.输入":wq",注意是冒号+wq,按回车键即可
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
### 优化的原则
- 多使用内存、缓存或者其他方法
- 减少CPU计算，减少请求
### 优化的入口
- 加载页面和静态资源
- 页面渲染
### 加载资源的优化
- 静态资源的压缩合并 js css img  比如webpack
- 静态资源缓存 一般浏览器都有自己的缓存，比如文件的名字没变，浏览器都不再去请求 比如mainfestion
- 使用CDN让资源加载更快  让CDN最近的机房给你返回结果
- 使用SSR后端渲染，数据直接输入到HTML   比如接口直接返回css，js，html
### 渲染优化
- css放前面，js放后面
- 懒加载（图片懒加载，下拉加载更多）
下面来讲下图片懒加载的原理
```bash
<img class="img1" src data-img="abc.png" />
<script>
 var img1 = document.getElementById('img1')
 img1.src = img1.getAttribute('date-img')
</script>
```
- 减少DOM查询，对DOM查询作缓存
```bash
//DOM查询无缓存
var i
for (i = 0; i< document.getElementsByTagName('p').length; i++) {
}

//DOM查询有缓存
var i
var pList = document.getElementsByTagName('p')
for (i = 0; i< pList.length; i++) {
}
```
- 减少DOM操作，比如插入10个数据，先造好数据再一起插入
- 事件节流
```bash
//-.throttle原理
var textarea = document.getElementById('map')
var timeoutId
textarea.addEventListener('drag', function () {
   if (timeoutId) {
   	clearTimeout(timeoutId)
   }
   
   timeoutId = setTimout(function () {
   	//change事件
   }, 100)
})
```
- 尽早执行操作（DOMContentLoaded）
```bash
window.addEventListener('load', function () {
	//页面所有的资源全部加载完才可以，包括图片，视频，字体等异步资源加载
})
document.addEventListener('DOMContentLoaded', function () {
	//只需要DOM加载完便可，此时的图片，视频或者字体等异步资源可能还没加载完
})
```
## 怎么保证程序的安全性
### XSS跨站请求攻击
- 比如用户提交反馈意见的时候，直接插入一段`script`，获取cookie密码等发送到自己的服务器
- 解决方法
  - 前端替换关键字，比如script
  - 后端替换
### XSRF跨站请求伪造
- 你已经登录一个网站购物，正在浏览商品，但是账户没有绑定验证，也就是可以直接无感付款，坏人直接获取你的信息，然后发送一封邮件给你，这时候你收到一个邮件，邮件里面有个很吸引人的图片，你点击图片的时候就往坏人的账户里面付了钱
- 解决方法
  - 增加验证流程，比如指纹、密码和短信验证

## 面试技巧
### 简历
- 简单明了，重点突出项目经历和解决方案
- 把个人博客放在简历中，并且定期维护和更新博客
- 把个人的开源项目放在简历中，并维护开源项目
- 简历千万不要造假，要保持能力和经历上的真实性
### 面试过程中回答
- 加班  临时加班可以，常态加班就不行，因为平时要自我学习提高
- 千万不要挑战面试官，尤其是不要反问面试官
- 学会给面试官惊喜，但不要太多，也就是回答面试官的一个问题迁出另外一个问题
- 遇到不会回答的问题，说出你知道的也就可以
- 谈谈你的缺点-------说一下你最近正在学的什么就可以了
