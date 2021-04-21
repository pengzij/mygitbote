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
9. 或者可以手动对这段代码进行修改，然后 git add .  //  git commit //然后终端会跳转


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