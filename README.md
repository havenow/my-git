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

# Github 团队协作流程图(forking工作流)
![](https://github.com/wangding/courses/blob/master/images/forkProcess.png)

# Git 使用规范流程    
[Git 使用规范流程](http://www.ruanyifeng.com/blog/2015/08/git-use-process.html)   

增加远程仓库，并命令 `git remote add [shortname] [url]`   

![Git使用规范流程](https://github.com/havenow/my-git/blob/master/images/Git%20Protocol.png)
