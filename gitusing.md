## git一个新的项目，初始化和上传 ##
1. git init
2. git add .
3. git remote add origin https://github.com/pengzij/mygitbote.git
4. git branch -M main//确认你的分支是main/ master
5. git push -u origin main  //上传到main/ master这个分支中

## 对已有项目修改和提交 ##
1. git push origin master//把修改后的上传到master/main，注意如果master还是空的，执行该修改语句则会报错
2. git push origin v1.0//上传当前项目，同时加上版本号

## 分支相关 ##
1. git branch main//创建main分支
2. git branch//显示所有分支，和当前你所在的分支
3. git checkout main//切换到main分支
4. git branch -d main//删除main分支
5. git checkout -b main//创建main分支并且跳转到main分支
6. git checkout -D main//强制删除
7. git merge main//把main分支和当前所在分支合并，原本main的分支不受影响
8. git merge --abort//如果合并分支时，出现冲突如下图，该语句为保留current change,忽略其他分支。
[![cbSDoV.png](https://z3.ax1x.com/2021/04/21/cbSDoV.png)](https://imgtu.com/i/cbSDoV)
9. 或者可以手动对这段代码进行修改，然后 git add .  //  git commit //然后终端会跳转到编辑文本vim界面，在空行处编辑这次修改的注释即可，i进入插入模式, esc命令模式，修改完成后命令模式下输入:wq,保存写入并退出即可.

## git ##
1. git checkout -- test.cpp //还原该文件到上次提交
2. git reset HEAD test.cpp //将该文件从暂存区中取
3. git rm test.cpp //删除文件
4. git mv test.cpp .\home\test.cpp //重命名文件，或移动文件
5. git reset --hard HEAD^ //整个项目回滚版本，回到上n个commit的版本(HEAD后面的^可以有n个)
6. git reset --hard 8e1b577da4353e618ed358f46ed5ba567f8b04b9//整个项目回退版本到输入log中对应版本的编号，可以只输入前7位
7. git checkout 8e1b577da4353e618ed358f46ed5ba567f8b04b9 -- version.cpp//只把选择version.cpp文件回退到该log对应版本
8. git tag v1.0//对上一次的修改加上tag
9. git tag//显示当前的tag
10. git tag v0.5 8e1b577da4353e618ed35 //对某一次的修改加上tag
11. git tag -d v0.5//删除v0.5的tag
12. git log --oneline//简略显示log
13. git log --graph//图表显示
14. git log --oneline --graph//简略图表显示

## 多人分支集成操作 ##
不同的人对项目修改：
1. git clone https://github.com/pengzij/mygitbote.git // 在github上项目的code按钮上获取对应的地址
2. git config --add --local user.name 'pzj' //配置本地项目的第二个人
3. git config --add --local user.email 'pzj@qq.com' //配置对应的邮箱
4. git config --local --list //可以查看是否配置成功
5. git branch -av //查看所有的分支
6. git checkout -b main remotes/origin/main //创建本地分支 main和远程分支 main做关联

1. git fetch// 将远程主机的最新内容拉取到本地，用户检查后决定是否合并到本地。git pull 是直接拉取并合并
2. git branch -av//查看所有分支信息，包括本地和远程的, 绿色的是本地的分支，红色的是远端的分支
3. git push origin --delete test//删除远程github上的test分支
 