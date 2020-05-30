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

