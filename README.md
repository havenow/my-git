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

# cherry pick
```
git cherry-pick -sx <commit_id>
cherry-pick 可以合并其它分支已有的提交（本地提交或远程提交），它有以下参数：
• -x 在提交信息的末尾追加一行（cherry picked from commit commit-id）
      方便以后查到这个提交是如何产生的，如果你合并的是一个远程仓库的提交，那么建议加上这个参数。
• -s 在提交信息的末尾追加一行操作者的签名(Signed-off by:xxx<邮箱>)，表示是谁进行了这个操作。
• -e 合并之后提交之前，打开外部编辑器，编辑自动生成的提交信息。一般不需要使用这个参数去编辑提交信息。

使用..合并多个连续的提交
左开右闭区间，不会包含 commit_a
git cherry-pick <commit_a>..<commit_b>

左闭右闭区间，包含commit_a
git cherry-pick <commit_a>^..<commit_b>


git cherry-pick一个merge提交（可以理解为空提交）
➜ git cherry-pick -x commitID-xxx
error: commit commitID-xxx is a merge but no -m option was given.
fatal: cherry-pick failed

cherry-pick A相当于把A^到A的变化应用于当前分支，如果A是merge的commit，A有两个父节点，那么就无法确定A^。
merge提交有两个parent，查看提交记录
提交：
commitID-xxx
父级：
commitID-xxx parent1, parent2

git cherry-pick -m 确实会将指定的合并提交应用到当前分支，并将其视为一个普通的提交，而不会保留中间的提交记录。这是因为 git cherry-pick 是基于提交的差异进行的，而不是基于分支的历史记录。
如果你需要保留中间的提交记录，并将整个分支的更改应用到当前分支，可以考虑使用其他的 Git 命令，如 git merge 或 git rebase。
```

# 打patch
```
git format-patch -1 commitSHA
git am --keep-cr --reject xxxx.patch  
git am --continue

# 生成最近一次提交的 patch
git format-patch HEAD~

# 打入 patch 并生成提交
git am --keep-cr xxx.patch

# 仅打入 patch 而不会生成提交
git apply xxx.patch
```

# 历史记录
```
开发过程中建议使用可视化工具查看日志
git log --pretty=format:"%ai , %an: %s" --since=“2022-08-26” >> ./20221025commit.log
git log --pretty=format:"%H, %ai , %an: %s" --since=“2022-08-26” >> ./20221025commit.log   %H添加commit id

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

git log一般第1行写简要说明，然后空行，再写详细说明.(开源项目都是这么做的，第1行作为主体，其它作为正文)
这样就能使用pretty能输出简要或详细模式的日志，空行是个比较关键的地方。
git log --pretty=oneline
git log --pretty=short
   oneline, short, medium, full, fuller, reference, email, raw
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

# msic
```
git pull --rebase
这样可以线性的看到每一次提交，并且没有增加提交节点

git merge --no-ff branch 
历史纪录会多出一个合并节点，为了保证版本演进的清晰，一般希望采用非快进合并
 With --ff, when possible resolve the merge as a fast-forward (only update the branch pointer to match the merged
           branch; do not create a merge commit). When not possible (when the merged-in history is not a descendant of the
           current history), create a merge commit.
使用 -ff 选项时，只有在要合并的分支的提交历史是当前分支的直接后继时，才会进行快进合并，不会创建新的合并提交。而在其他情况下，无论是否使用 -ff 选项，都会创建一个新的合并提交。
直接后继的场景在实际开发中基本不可能遇到，下面是直接后继的例子。
      A--B--C   feature
      /
D--E--F         master
git checkout master; git merge feature之后（默认是--ff）会变成：
      A--B--C   feature
      /         master
D--E--F         


git reset --soft HEAD^ 
将最近一次commit的代码放回到暂存区，改操作不会影响到工作区
commit代码后发现需求继续修改时，将代码从本地仓储退回到暂存区

git reset --hard HEAD
丢弃掉工作区和暂存区的所有改动

git reset --hard HEAD^
丢弃掉工作区、暂存区、最新一次提交。
使用场景：commit了修改，还没有push，此时想回到上一次提交的初始状态。

git commit -t /Users/xxx/Documents/commit-template
       -t <file>, --template=<file>
提交时会根据指定文件中的内容编辑器，可以在编辑器中国呢修改提交记录，如果记录未做修改，提交将终止。
例子：commit-template文件内容如下
#【项目：】本次提交的简要说明，说明本次提交干了什么，记得空一行，方便git log的pretty输出
【项目：】

# 本次提交的原因
【原因：】
# 本次提交的改动内容
【改动：】
```
