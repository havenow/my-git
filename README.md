# my-git
git相关资料

# 使用github    
[极客学院：github使用手册](http://wiki.jikexueyuan.com/project/github-basics/)

# Git命令   

- [ProGit v2](https://git-scm.com/book/zh/v2)    
- [常用 Git 命令清单（阮一峰）](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)     
- [Git 图解剖析](http://www.cnblogs.com/yaozhongxiao/p/3811130.html)    

git 模型可以抽象为：    
远程仓库——remote    
本地三级仓库: level1——working directory    level2——stage(index)    level3——repository(History) 

|            |      低level输入        | 高level 输入  |   
| ------------- |:-------------:| -----:|   
| working directory      | 手工创建 | git checkout/git stash |  
| stage(index)      | git add      |   git reset |    
| History(repository) | git commit      |    git pull |   
| remote | git push      |    - |   

# Git工作流    
[Git工作流指南](https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md)

# Git Flow工作流   
![](https://github.com/havenow/my-git/blob/master/images/my-workflow-cycle.png)

# Github 团队协作流程图(forking工作流)
![](https://github.com/wangding/courses/blob/master/images/forkProcess.png)

# Git 使用规范流程    
[Git 使用规范流程](http://www.ruanyifeng.com/blog/2015/08/git-use-process.html)   

增加远程仓库，并命令 `git remote add [shortname] [url]`   

![Git使用规范流程](https://github.com/havenow/my-git/blob/master/images/Git%20Protocol.png)

# 根据官方项目创建自己的版本，同时更新官方代码到自己的版本（不做request）
```
1. Fork
2. git clone https://github.com/your_id/mameui（此时clone到的是最新版本的官方代码）
   如果需要切换到某个历史版本(需求：当初在某个历史版本修改的，现在回退到该版本，做合并后在pull官方的代码)
   git reset --hard 历史版本的id
   git push -f -u origin master
3. git remote add upstream https://github.com/Robbbert/mameui
4. 在本地修改代码，
   git add .
   git commit -m "commit message"
   git push origin master(先push到自己的远程仓库，才能pull官方的远程仓库)
5. git pull upstream master
   此时需要修改代码的冲突，修改完冲突，在push代码到自己的远程仓库
```
