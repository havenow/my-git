Gitflow工作流仍然用中央仓库作为所有开发者的交互中心。

[A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)     
[一个成功的 Git 分支模型 ](https://www.oschina.net/translate/a-successful-git-branching-model?lang=chs&page=1#)
![](https://github.com/havenow/my-git/blob/master/images/git-flow.png)   

# 这张图左转90度，就容易理解了。
![](https://github.com/havenow/my-git/blob/master/images/git-workflow-release-cycle.png)   

- # master分支				
也叫production分支，存储了正式发布的历史。 	
这个分支只能从其他分支合并，不能在这个分支直接修改。				

- # develop分支				
作为主开发分支。		

- # feature 分支		
(从develop分支checkout，合并回develop分支)
功能分支，用来开发一个新的功能，一旦开发完成，合并回develop分支进入下一个release。	
功能分支不是从master分支上拉出新分支，而是使用develop分支作为父分支。当新功能完成时，合并回develop分支。			

- # release分支		
（从develop分支checkout，合并回develop分支和master分支）	
这个分支只应该做Bug修复、文档生成和其它面向发布任务。				
发布一个新release的时候，我们基于develop分支创建一个release分支，完成release后，我们合并到master和develop分支，master分支应该用新的版本号打好Tag。。

- # hotfix分支		
（从master分支checkout，合并回develop分支和master分支）	
维护分支，用于生成快速给产品发布版本打补丁，这是唯一可以直接从master分支fork出来的分支。 
修复完成，修改应该马上合并回master分支和develop分支，master分支应该用新的版本号打好Tag。		

master和develop分支是长期分支；
feature,release和hotfix分支都是临时分支，可以删除。

[Git 在团队中的最佳实践](http://www.cnblogs.com/cnblogsfans/p/5075073.html)


![实操](https://github.com/havenow/my-git/blob/master/images/gitflow%E5%B7%A5%E4%BD%9C%E6%B5%81%E5%AE%9E%E6%93%8D.png)
