# GitHub使用    
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
[参考文档：Git工作流指南](https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md)

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

#  配置了密钥到Github上，提交代码还是要输入用户名和密码
```
因为用的是https而不是ssh，更新origin为ssh格式即可。
https的格式为：https://github.com/用户名/仓库名.git
ssh的格式为：git@github.com:用户名/仓库名.git

解决方法：
git remote remove origin
git remote add origin git@github.com:用户名/仓库名.git
```

# Git 帮助文档
```
git <command> help   输出简短的参数选项
git help <command>   输出详细说明
```

# 打patch
```
git format-patch -1 commitSHA
git am --keep-cr --reject xxxx.patch  
git am --continue
```

# 历史记录
```
开发过程中建议使用可视化工具查看日志
git log --pretty=format:"%ai , %an: %s" --since=“2022-08-26” >> ./20221025commit.log

git log -S <string>
-S参数接受一个字符串参数，用来显示那些添加或删除了该字符串的提交

git log -- <path>
在 git log 的最后指定文件名或者目录并用--隔开，则可以只看到文件或者目录的历史改动。
如果这个文件被删除了，则可以用来查找这个文件是何时被删除的。

git blame -L 100,106 xxx.cpp
可以追踪代码里面的每一个改动
使用-L参数还可以限制文件中的代码行，默认是所有行

git log --stat          快速浏览某提交所带来的变化
git log --patch -n      显示最近n次提交所引入的差异（按 补丁 的格式输出）
git show commitID       查看commitID所引入的差异（按 补丁 的格式输出）
```

```
在代码提交到远程仓库之前，我们都可以在本地随便修改历史记录。
一旦将代码推送到了远程仓库，那么除非特殊情况，都不建议直接修改远程仓库的历史记录。

修改最后一次提交，或是仅修改最后一次提交的提交信息
git commit --amend

修改多个提交
如果你的本地代码里面有多个提交，而你想要修改的提交记录并不是最近的那条提交。
Git 其实并没有一个改变历史记录的工具，但是却可以利用变基命令来变基一系列提交。
通过变基命令，可以在任何想要修改的提交后停止，然后修改信息、添加文件或做任何想做的事情。
通过给git rebase增加-i选项来指定想要重写多久远的历史。

git rebase -i HEAD~n
git rebase -i HEAD~3 修改最后三次提交

p, pick <commit> = use commit                                  直接使用提交
r, reword <commit> = use commit, but edit the commit message   修改提交信息
e, edit <commit> = use commit, but stop for amending           修改相应的提交
s, squash <commit> = use commit, but meld into previous commit 合并提交
d, drop <commit> = remove commit                               删除提交

可以调整提交的顺序来达到重新排序提交的目的，删除提交行则可以删除相应的提交。
将提交前面的pick改为edit，就可以修改相应的提交。
变基命令重新应用提交时，遇到edit的提交就会停下来，等待你完成修改。
      你可以调整你的改动，或只是调整提交信息，当完成修改后，运行git rebase --continue就可以继续变基命令。
      （停下来后，修改代码，git add; git commit --ammend; git rebase --continue）
使用squash参数合并提交。
使用reword参数来修改某次改动的提交信息。
使用edit参数并结合git reset命令来拆分一个很大的提交。
注意：使用git rebase时需要stash本地工作区。
```

# 贮藏改动
```
贮藏改动
git stash

也会贮藏未跟踪的文件（不会包含已忽略的文件）
git stash -u

贮藏列表
git stash list

应用最近一次贮藏的改动
git stash apply

应用最近一次贮藏的改动，并将这条贮藏改动从栈上丢弃
git stash pop

应用 stash@{2} 的贮藏改动
git stash apply stash@{2}

丢弃最近一次贮藏的改动
git stash drop

丢弃 stash@{2} 的贮藏改动
git stash drop stash@{2}

丢弃所有的贮藏改动，即清空栈
git stash clear

查看stash@{0}的记录
git stash show stash@{0}      粗略的查看，列出有修改的文件
git stash show stash@{0} -p   详细的查看，以patch的格式显示

指定说明文字
git stash push -m "stash message"

交互式stash，每个修改逐个确认，之后不停按y/n来选择要stash的修改
如果接下来没有需要stash的文件,则直接q退出就行
git stash push -p -m "stash message"     目前发现会跳过修改过的png文件，估计二进制文件都会跳过
git stash -p -m "stash message" 也可以

指定文件列表stash，需要指定文件的路径，可以通过git status获取文件路径
先将需要暂存的文件放入staged区，然后git status，拷贝文件路径比较方便
git stash push ***.cpp ***.h -m "stash message"
```
