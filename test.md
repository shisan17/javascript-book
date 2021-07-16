具体方法操作如下：

1、首先通过 git remote -v 查看您要同步的仓库的远程库列表，如果在列表中没有您 Gitee 的远程库地址，您需要新增一个地址

git remote add 远程库名 远程库地址
eg: git remote add gitee git@github.com:xxx/xxx.git
如果在 add 的时候出现error: Could not remove config section 'remote.xxx'.一类的错误，通过把仓库下.git/config 文件里面的 [remote "xxx"] 删掉或者是用别的远程库名即可。

2、从 GitHub 上拉取最新代码到本地

git pull 远程库名 分支名
eg：git pull origin master
3、推送本地最新代码到 Gitee 上