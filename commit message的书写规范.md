[阮一峰：Commit message 和 Change log 编写指南](https://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)    

# Commit message 的格式
每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。   
```
<type>(<scope>): <subject>    
// 空一行    
<body>    
// 空一行    
<footer>    
```
其中，Header 是必需的，Body 和 Footer 可以省略。

## Header   
Header部分只有一行，包括三个字段：type（必需）、scope（可选）和subject（必需）。   
- ### type    
type用于说明 commit 的类别，只允许使用下面7个标识。    

feat：新功能（feature）   
fix：修补bug   
docs：文档（documentation）    
style： 格式（不影响代码运行的变动）   
refactor：重构（即不是新增功能，也不是修改bug的代码变动）    
test：增加测试   
chore：构建过程或辅助工具的变动    
如果type为feat和fix，则该 commit 将肯定出现在 Change log 之中。其他情况（docs、chore、style、refactor、test）由你决定，要不要放入 Change log，建议是不要。

- ### scope   
scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

- ### subject   
subject是 commit 目的的简短描述，不超过50个字符。

以动词开头，使用第一人称现在时，比如change，而不是changed或changes
第一个字母小写
结尾不加句号（.）

## Body   
Body 部分是对本次 commit 的详细描述，可以分成多行。

2.3 Footer

##  Footer 部分只用于两种情况。   
（1）不兼容变动    
如果当前代码与上一个版本不兼容，则 Footer 部分以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法。    
（2）关闭 Issue   
Closes #234
