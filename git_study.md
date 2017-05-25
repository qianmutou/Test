# 笔记 #
1. 解决fatal: Could not read from remote repository.Please make sure you
1.  have the correct access rights and the repository exists.问题——————原因是github账户里没添加SSH key，加入即可
1. 步骤：输入 ssh-keygen -t rsa -C "username" (注：username为你git上的用户名). 一路回车，最后会告诉你id_rsa.pub在哪，打开，把所有字符串都复制到github账户里，再remote即可。
1. 第一次提交仓库，除了add 和 commit 命令外，还有 remote add 命令和push -u命令。之后，只需要add commit push三个命令即可。
1. 重启电脑后再打开Git Bash，需要先cd到当前git目录，并重新初始化，然后再添加
1. 一次性添加多个文件，注意别把ssh码等私密信息也加进去
1. 向github添加一个项目，先在github新建一个同名仓库，然后cd到本地这个项目目录，init.然后add
1.  commit remote push即可。
2.  github手机版，txt格式中文有乱码，考虑改为md文件，又有格式，还能加超链接和图片。




----------
# 代码 #

    cd learngit
    cd test			
	cd ~//进入工作目录
	cd.. //上一层目录 
    git add git_study.txt
    git commit -m"anything you want"
    git push -u test master
    git push test master
    git add --all//添加当前目录下的所有文件 
    git remote add test git@github.com:qianmutou/learngit.git

2017/5/25 16:38:00 

