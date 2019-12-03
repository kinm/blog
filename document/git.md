## 配置git用户名和密码

```shell
$ git config --global user.name "<用户名>"
$ git config --global user.email "<电子邮件>"
```

## 让git以彩色显示

```shell
$ git config --global color.ui auto 
```

## 为git命令设置别名

```shell
$ git config --global alias.co checkout
```

## 初始化git库

```shell
$ git init
```

## 确认工作树和索引的状态

```shell
$ git status
```

## 指定加入索引的文件

```shell
$ git add <filename>  // 加入指定文件
// or
$ git add . // 加入当前目录下的所有文件
```

## 提交文件

```shell
$ git commit -m "<提交注解>"
```

## 查看提交记录

```shell
$ git log
```

## 指定远程git数据库

```shell
$ git remote add origin <url>
```


## 向Git库推送更改内容

```shell
$ git push
//or
$ git push <repository> <refspec>  //<repository>处输入目标地址，<refspec>处指定分支
//or
$ git push -u origin master
```

## 克隆远程git数据库

```shell
$ git clone <repository> <directory> // <repository>指定远程数据库的URL，在<directory>指定新目录的名称
```

## 从远程数据库拉取最新变更内容

```shell
$ git pull <repository> <refspec> //<repository>处输入目标地址，<refspec>处指定分支
// or
$ git pull origin master
```

## 建立分支branch

```shell
$ git branch <branchname>
```

## 显示分支列表

```shell
$ git branch
```

## 切换分支

```shell
$ git checkout <branch>
```

## 创建分支并进行切换

```shell
$ git checkout -b <branch>
```

## 合并分支

```shell
$ git merge <branchname>
```

## 删除分支

```shell
$ git branch -d <branchname>
```

## 重设分支合并

```shell
$ git rebase --hard HEAD~ //rebase的时候，修改冲突后的提交不是使用commit命令，而是执行rebase命令指定 --continue选项。若要取消rebase，指定 --abort选项。
```

## 修改最近的提交

```shell
$ git commit --amend
```

## 取消过去的提交

```shell
$ git revert HEAD
```

## 遗弃提交

```shell
$ git reset --hard HEAD~~
```

## 从其他分支复制指定的提交,导入到现在的分支

```shell
$ git cherry-pick 99daed2
```

> 欢迎收藏和提交issues讨论。[GitHub地址](https://github.com/kinm/kinm.github.io/issues)