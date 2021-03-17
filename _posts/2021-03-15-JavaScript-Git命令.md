# Git命令

    分布式版本控制系统
    检查版本 `git --version`
    初始化`git init`

## 配置用户信息

    `$ git config --global user.name "damu"`
    
    `$ git config --global user.email"damu@example.com"`
    
    要检查已有的配置信息：`$ git config --list`
    
    /etc/gitconfig文件：系统中对所有用户都普遍适用的配置。若使用`$ git config --system`，读写的就是这个文件。

    ~/.gitconfig文件：用户目录下的配置文件只适用于该用户。若使用`$ git config --global`，读写的就是这个文件。

    .git/config文件：当前项目的Git目录中的配置文件（也就是工作目录中的.git/config文件）这里的配置仅仅针对当前项目有效。

## 区域

    工作区
    暂存区
    版本库

![图片alt](images/1.png "图片title")

## 对象

    Git对象
       git hash-object -w fileUrl : 生成一个key(hash值):val(压缩后的文件内容)存到 .git/objects
    tree对象
       git update-index --add --cacheinfo 100644 hash test.txt : 往暂存区添加一条记录(让git对象对应上文件名)
       git write-tree : 生成树对象
    commit对象
       echo "first commit" | git commit-tree treehash : 生成一个提交对象
    对以上对象的查询：
           git cat-file -p hash  : 拿对应对象的内容
           git cat-file -t hash  : 拿对应对象的类型
    查看暂存区：git ls-files -s
![图片alt](images/2.png "图片title")

## 基础的Linux命令

    clear：清除屏幕
    echo 'test content'：往控制台输出信息 echo 'test content' > test.txt
    ll：将当前目录下的子文件&子目录平铺在控制台
    find目录名：将对应目录下的文件平铺在控制台
    rm文件名：删除文件
    mv源文件 重命名文件：重命名
    cat文件的url：查看对应文件的内容
    vim文件的url(在英文模式下)
        按i进入插入模式  进行文件的编辑
        按esc键&按:键  进行命令的执行
        q! 强制退出(不保存)
        wq 保存退出
        set su 设置行号

## git对象

    key:val 组成的键值对(key是val对应的hash)
    键值对在git内部是一个blob类型

    `ehco "test contect v1" > test.txt`
    `git hash-object -w ./test.txt`

    问题： 1.记住文件的每一个版本所对应的SHA-1值并不现实
           2.在Git中，文件名并没有被保存--仅保存了文件的内容

           解决方案:树对象

## 高层命令

    git ./add  的工作流程是  先到版本库再到暂存区

    git操作最基本流程：
         1. 创建工作目录 对工作目录进行修改
         2. git add ./    
              git hash-object -w 文件名(修改了多少个工作目录的文件 此命令就要执行多少次)
              git update-index ...
         3. git commit -m "注释内容"
              git write-tree
              git commit-tree

### git高层命令（CRUD）

`git version`               检查版本
`$ git config --global user.name "damu"`
    `$ git config --global user.email"damu@example.com"`
    `git config --list`        初始化配置
    `git init`                初始化仓库

### C(新增)

在工作目录中新增文件
`git status`检查状态
`git add ./`              将修改添加到暂存区
`git commit -m "注释"`    将暂存区提交到版本库

### U(修改)

在工作目录中修改文件
`git status`检查状态
`git add ./`              将修改添加到暂存区
`git commit -m "注释"`    将暂存区提交到版本库

### D(删除 & 重命名)

`git rm 文件名`            删除工作目录中对应的文件 再将修改添加到暂存区
`git mv` 原文件名 新文件名 将工作目录中的文件进行重命名 再将修改添加到暂存区
`git status`检查状态
`git add ./`              将修改添加到暂存区
`git commit -m "注释"`    将暂存区提交到版本库

### R(查询)

`git status`  : 查看工作目录中文件的状态(已跟踪 未跟踪)
`git diff` : 查看未暂存的修改
`git diff -cache/staged` : 查看未提交的暂存
`git diff HEAD -- ***.txt` : 查看工作区和版本库里最新版本的区别
`git log --oneline` : 查看提交记录
`git log --oneline --decorate --graph --all` : 查看整个项目的分支历史

       git commit
       git commit -a           跳过暂存区
       git commit -a -m "注释"  

## Git分支操作

    分支的本质其实就是一个提交对象
    HEAD：是一个指针 它默认指向main分支 切换分支时，其实就是让HEAD指向不同的分支 每次有新的提交时 HEAD都会带着当前的分支一起向前移动

    git log --oneline --decorate --graph --all    查看分支列表
    git branch                  显示分支列表
    git branch 分支名           创建分支(在当前提交对象上创建新的分支)
    git branch 分支名 commithash (在指定的提交对象上创建新的分支)
    git checkout 分支名         切换分支
    git branch -d 分支名      删除已经完成(合并)的分支
    git branch -D 分支名      强制删除分支

    ***切换分支：
          最佳实践：每次切换分支前 当前分支一定得是干净的(已提交状态)
          坑：在切换分支时 如果当前分支上有未暂存的修改(第一次) 或者 有未提交的暂存(第一次) 分支可以切换成功 但是这种操作可能会污染其他分支
          动三个地方： HEAD
                      暂存去
                      工作目录
小结：

Git鼓励大量使用分支：

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>或者git switch <name>`

创建+切换分支：`git checkout -b <name>或者git switch -c <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`

查看分支合并图：`git log --graph --pretty=oneline`

补充：

    通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。

    如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

    git merge --no-ff -m "merge with no-ff" dev

    分支策略:
    在实际开发中，我们应该按照几个基本原则进行分支管理：
    首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
    那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
    你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

BUG分支：

    1.用`git stash`把当前工作现场储藏起来
    2.`git checkout 分支`确定bug的位置 并切换到bug所在分支
    3.在bug所在分支创建新的分支  修复bug后 合并并提交
    4.删除issue-101分支
    5.使用`git stash list`命令查看刚刚储藏起来的工作
    6.用git stash pop恢复
    7. 我们修复的bug可能在其他分支也有问题 我们可以直接使用`git cherry-pick 4c805e2` 复制一个特定的提交到当前分支

小结
修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

多人协作：
`git remote`       查看远程库的信息
`git remote -v` 详细信息
`git push origin master` 把分支推送到远程库
抓取分支：
1.`git clone git@github.com:zhaoyuhui328/learngit.git` 链接到远程
2.`git branch -b dev origin/dev`创建远程origin的dev分支到本地
3.在dev上修改后，把dev分支push到远程 `git push origin dev`
4.如果推送失败  `git pull` 抓取
5.`git branch --set-upstream-to=origin/dev dev`指定本地dev分支与远程origin/dev分支的链接
6.再pull
7.手动解决完冲突后 在push提交

因此，多人协作的工作模式通常是这样：

首先，可以试图用`git push origin <branch-name>`推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

小结
查看远程库信息，使用`git remote -v`；

本地新建的分支如果不推送到远程，对其他人就是不可见的；

从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；

在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；

建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；

从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

## 标签管理

`git tag <tagname>` 建立一个标签，默认为`HEAD`，也可以指定一个`commit id`；
`git tag -a <tagname> -m "balabala"` 可以指定标签信息；
`git tag` 可以查看所以标签
`git tag -d <tagname>` 删除标签
`git push origin <tagname>` 推送某个标签到远程
`git push origin --tags` 一次性推送全部尚未推送到远程的本地标签
要删除远程标签 <1>`git tag -d <tagname>`先从本地删除
<2>`git push origin :refs/tags/<tagname>`然后从远程删除

小结
命令`git push origin <tagname>`可以推送一个本地标签；

命令`git push origin --tags`可以推送全部未推送过的本地标签；

命令`git tag -d <tagname>`可以删除一个本地标签；

命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。

## Git后悔药(版本回退)

    git reset --hard HEAD^    回退到上一个版本
    git reset --hard 1094a    hard后面是未来版本的 commit id
    git reflog                记录操作的每一步命令(主要作用是查看commit id)  称为git时光机
    
    小结:
         HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。

         穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

         要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
    
    补充： 
        git checkout -- readme.txt 把readme.txt文件在工作区的修改全部撤销
        git reset HEAD <file>      撤销暂存区的修改，然后执行第一步

        小结：
            场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

            场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

            场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

## 远程仓库

一.添加远程库
1.首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：
    ![图片alt](images/0.png "图片title")
2.在Repository name填入learngit，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：
![图片alt](images/3.png "图片title")
3.在本地仓库下运行命令：
git remote add origin git@github.com:zhaoyuhui328/learngit.git
4.将本地库中的内容推送到远程库上：
git push -u origin master

!!!SSH警告
当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：

    The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
    RSA key fingerprint is xx.xx.xx.xx.xx.
    Are you sure you want to continue connecting (yes/no)?
这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

    Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
这个警告只会出现一次，后面的操作就不会有任何警告了。

如果你实在担心有人冒充GitHub服务器，输入yes前可以对照GitHub的RSA Key的指纹信息是否与SSH连接给出的一致。

删除远程库
如果添加的时候地址写错了，或者就是想删除远程库，可以用git remote rm name命令。使用前，建议先用git remote -v查看远程库信息：

    $ git remote -v
    origin  git@github.com:michaelliao/learn-git.git (fetch)
    origin  git@github.com:michaelliao/learn-git.git (push)

然后，根据名字删除，比如删除origin：

    git remote rm origin

此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。

小结:

要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；

关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步，真是太方便了！

二.从远程克隆
`$ git clone git@github.com:zhaoyuhui328/gitskills.git`

Git支持多种协议，包括https，但ssh协议速度最快。

`$ git config --global alias.st status` 配别名

参考文献：<https://www.liaoxuefeng.com/wiki/896043488029600>
廖雪峰老师的官方网站
