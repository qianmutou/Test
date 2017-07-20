# 笔记 #
- 解决fatal: Could not read from remote repository.Please make sure you
-  have the correct access rights and the repository exists.问题——————原因是github账户里没添加SSH key，加入即可
- 步骤：输入 ssh-keygen -t rsa -C "username" (注：username为你git上的用户名). 一路回车，最后会告诉你id_rsa.pub在哪，打开，把所有字符串都复制到github账户里，再remote即可。
- 第一次提交仓库，除了add 和 commit 命令外，还有 remote add 命令和push -u命令。之后，只需要add commit push三个命令即可。
- 重启电脑后再打开Git Bash，需要先cd到当前git目录，并重新初始化，然后再添加
- 一次性添加多个文件，注意别把ssh码等私密信息也加进去
- 向github添加一个项目，先在github新建一个同名仓库，然后cd到本地这个项目目录，init.然后add
-  commit remote push即可。
- 2.  github手机版，txt格式中文有乱码，考虑改为md文件，又有格式，还能加超链接和图片。
- 3.  把别人的项目复制到你的账户-------在他的源码界面点击fork按钮就行
- 把文件克隆到本地的步骤：
- 1，cd到你想要克隆的本地目录
- 2，git init 
- 3，按照以前的步骤把新的ssh添加到网页的github账户里 
- 4，git clone git@github.com:qianmutou/test.git    这样就把test仓库的所有文件都克隆到本地了
- 的




----------
# 代码 #

    cd learngit
    cd test			
	cd ~//进入工作目录
	cd .. //上一层目录 
	git init  //把当前目录初始化为git可管理的目录
    git add git_study.txt
    git commit -m"anything you want"
	git remote add test git@github.com:qianmutou/learngit.git //第一次把本地仓库和账号里的仓库关联，准备提交
    git push -u test master
    git push test master
    git add --all//添加当前目录下的所有文件 
    

2017/5/25 16:38:00 

