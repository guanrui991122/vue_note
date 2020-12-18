# 4.

## .3分支操作

### .1创建分支

git branch 分支名称

### .2查看分支

git branch -v

### .3切换分支

git checkout 分支名称

### .4合并分支

#### .1切换到将被修改的分支（被合并，增加新的内容）

git checkout 被修改分支名称

#### .2执行merge命令

git merge 要被添加到被修改分支中的分支的名称

### .5解决冲突分支

#### .1编辑文件，删除特殊符号

#### .2把文件修改到满意的程度，保存退出

#### .3 git add 文件名

#### .4 git commit -m"日志信息"

- 注意：此时后面不能带文件名称

## 5.

### .2添加远程地址并命别名

git remote add 别名 远程地址

```
举例为：
git remote add origin https://github.com/guanrui991122/huashan.git
```



### .3查看当前所有远程地址别名

git remote -v

### .4推送

git push 别名 分支名

```
举例为：
git push origin master
```

### .5克隆

#### .1作用

```
1.完整地把远程库下载到本地  
2.创建origin远程地址别名
3.初始化本地库
```

#### .2代码

```
git clone 远程地址
```

### .6拉取

`pull = fetch + merge`

```
git fetch 远程库地址别名 远程分支名
```

举例为：
git fetch origin master

```
git merge 远程库地址别名/远程分支名
```

举例为：
git merge origin/master

### .7解决冲突

`要点`

```
1.如果不是基于GitHub远程库的最新版所做的修改，不能推送，必须先拉取
2.拉取下来后如果进入冲突状态，则按照“分支冲突解决”操作解决即可
```

### .8 SSH免密登录

##### 1.进入用户的家目录

cd ~

##### 2.删除.ssh目录

rm -rvf .ssh

##### 3.运行命令生成.ssh密钥目剥

ssh-keygen -t rsa -C 1992503408@qq.com

###### [注意:这里-C这个参数是大写的C]

##### 4.进入.ssh目录查看文件列表

cd .ssh
Is -IF

##### 5.查看id_rsa.pub文件内容

cat id_rsa.pub

##### 6.复制id_rsa.pub文件内容,登录GitHub,点击用户头像→Settings-SSH and GPGkeys

##### 7. New SSH Key

##### 8.输入复制的密钥信息

##### 9.回到Git bash 创建远程地址别名

git remote add origin_ssh git@github.com:guanrui991122/huashan.git

##### 10.推送文件进行测试