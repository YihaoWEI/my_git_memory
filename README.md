# my_git_memory
Awesome git memories

## 关于Squash  
当我们开发的分支总是非常的杂乱的时候，我们需要把一连续commit压缩成1个，这样方便后续的rebase/merge操作等。使用方式是：
在你当前的**dev_branch**下    
```git rebase -i src_branch```  
src_branch即是你dev_branch切起的分支。通常，这个src_branch是master，因为我们都是基于master分支开发的。  
你会看到一个不太熟悉的编辑器，没关系，我们的目的是将**pick**转换为**squash**  
出了第一行的pick不能转squash，后面的都可以squash了。然后退出，再  
```git push -f```  
即可发现我们的commit都squash了。  
更常见的情况是，我们的master pull到了最新，可我们在老版本的master下切出了dev_branch。这个时候，如果直接使用上述命令行，则依然会很麻烦的要去解决冲突。解决方法就是，先将master退回我们分支切出时候的commit，然后进行squash，最后再一口气的rebase到最新，即可。  

此外，我们还可以 `git rebase -i HEAD~5`或者`git rebase -i <after-this-commit>`来进行同样的squash操作。  

## 关于"<<<<<<<<<<HEAD" "===========" 和 ">>>>>>>>> a1b2c3d4"  
这是代码共同修改了同一部分。其中，  
<<<<<<<<<<HEAD 与 =========== 之间的是当前分支修改的内容 ，而 =========== 和  a1b2c3d4 之间是要合入/变基的分支的内容。  

## 关于cherry-pick  
当我们的分支需要精确的去除一些错误的提交，并重新把我们之前做过的有效的提交实施时，我们需要cherry-pick。例如：  
当你的commit a与commit b(a 早于 b)应用在分支上，准备合入。但突然被告知，最新的10次commit(均早于commit a)都有问题，需要撤回。这时候，我们可以如下操作：  
```git log```  
找到commit a和commit b，记录下他们的git hash(hash-a hash-b)。并记录我们要回退到10次之前的commit，记为hash-r。然后  
```git reset --hard hash-r```  
这时，再log可以看到我们是否回退到了以前版本  
此时，使用**cherry-pick**，将commit a和commit b提交回来。可以连续使用两次（先a后b），也可以直接将a与b按顺序写好，例如：  
```git cherry-pick hash-a hash-b```  
再log查看，此时已经更新了。再git push -f即可。  

## 可视化的10大git命令  
可参考[源文](https://dev.to/lydiahallie/cs-visualized-useful-git-commands-37p1)与[译文](https://zhuanlan.zhihu.com/p/147356242?utm_source=wechat_session&utm_medium=social&utm_oi=26778592608256&s_r=0&from=singlemessage)探讨可视化的git的10大命令  




