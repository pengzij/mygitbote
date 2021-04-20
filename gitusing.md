## git一个新的项目，初始化和上传 ##
1. git init
2. git add .
3. git remote add origin https://github.com/pengzij/mygitbote.git
4. git branch -M main//确认你的分支是main/ master
5. git push -u origin main  //上传到main/ master这个分支中

## 对已有项目修改，继续提交master分支 ##
1. git push origin master//把修改后的上传到master/main，注意如果master还是空的，执行该修改语句则会报错

## git使用的相关快捷键 ##
1. git checkout -- test.cpp //还原该文件到上次提交
2. git reset HEAD test.cpp //将该文件从暂存区中取
3. git rm test.cpp //删除文件
4. git mv test.cpp .\home\test.cpp //重命名文件，或移动文件
5. git reset --hard HEAD^ //整个项目回滚版本，回到上n个commit的版本(HEAD后面的^可以有n个)
6. git reset --hard 8e1b577da4353e618ed358f46ed5ba567f8b04b9//整个项目回退版本到输入log中对应版本的编号，可以只输入前7位
7. git checkout 8e1b577da4353e618ed358f46ed5ba567f8b04b9 -- version.cpp//只把选择version.cpp文件回退到该log对应版本