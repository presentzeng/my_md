1. workspace --> git add --> stage --> git commit --> master(HEAD) --> git push --> remote
2. 只输入git diff查看的是workspace -- stage
3. 想看workspace和master可以输入git diff HEAD
4. HEAD指向本地master最新的提交点 HEAD^前一个 HEAD~100前100个
5. git checkout -- file 将该文件回到最近的一次git add or git commit状态,即用stage的覆盖workspace,要无修改才能切换
6. git reset HEAD file 将stage里面的也撤销成最近的一次commit,即用master覆盖stage
7. git rm 删除后需要git rm
8. git checkout -b xxx 创建分支, 不加b可以直接切换分支,但是同时会修改掉本地的东西
9. git merge xxx 将当前分支和xxx分支合并
10. git log --graph可以看到分支合并情况
11. git reset --hard commit号 commit回退
12. git reflog 查看所有log
13. git remote -v显示远程分支信息
14. git tag用于打tag 可加commit号,不加默认打最新的,可以用git show看tag

### tips
比方说有两个分支
dev 和 master
如果两个是指向一样的HEAD则可以随便checkout对方
但是只要有一方commit了,就直接记录在那方身上,此时还要checkout就要没任何改动
此时如果想去其他分支同时又不提交自己的东西可以先git stash,要的时候再git stash pop