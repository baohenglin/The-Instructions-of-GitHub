
## 1.Github 基本使用
    下面将从如何创建仓库、如何创建分支以及如何合并分支三方面介绍GitHub的基本使用。[Github基本使用](https://guides.github.com/activities/hello-world/)

    1、如何创建新的仓库？
         具体步骤：
            1、点击页面右上角的头像左侧的“+”，并在下拉菜单中选择“New repository”;
            2、在仓库名称输入框中编辑仓库名称，比如“Hello-world”；
            3、可以写一段简短的描述；
            4、注意勾选上“Initialize this repository with a README”;
            5、点击“Create repository”按钮即可创建完成。
  
    2、如何创建分支？
    创建仓库后默认生成一个名叫“master”的主分支，该主分支用来存储最终版本的代码。我们需要创建master的一个分支，在该分支上修改代码，确定之后再提交   到主分支。那么如何创建分支呢？
        具体步骤：
           1、首先进入“Hello-world”仓库；
           2、点击文件上方的“branch:master”的下拉菜单；
           3、输入分支名称“branchOne”；
           4、点击下方的分支创建按钮，即可完成分支的创建。
        
    3、如何合并分支代码？
        分支branchOne修改（增加的代码以绿色标出，删除的代码以红色标出）后，最后需要合并到主分支master。
        具体步骤：
           1、点击“Pull Request”按钮，切换到请求代码合并页面；
           2、点击右侧的“New pull request”按钮；
           3、选择创建的“branchOne”分支，并与主分支比较；
           4、在对比页面查看这些修改，并确定是否都合并到master分支；
           5、点击“Create Pull Request”按钮，并添加标题和描述；
           6、点击“Merge pull request”按钮，将branchOne分支的修改合并到主分支；
           7、点击“Confirm merge”按钮；
           8、点击紫色框中的“Delete branch”按钮，删除branchOne分支（因为branchOne分支的修改已合并到master分支）。
    
    以上就是如何在GitHub上创建仓库、创建分支、合并分支代码的基本操作步骤。
        
## 2.创建与"README.md"同级的文件夹

    如何建立与"README.md"同级的文件夹?点击“Create new file”，然后输入文件夹名称，此时在输入的名称后面加上"/"，然后再输入下一级文档的名称进行创建保存。注意一定要要在文件夹名称后面加上‘/’，否则创建出来的不是文件夹。这样就可以在该文件夹路径下上传.md的文档了。
   
## 3.删除仓库的影响 

删除“repositories”中的某个仓库之后,该仓库对应的commit记录也将一同被删除掉。

## 4.Changing author info

修改author信息，以前的提交记录的contributions将丢失。那么如何解决这一问题呢？

[Github官网解决方法](https://help.github.com/en/articles/changing-author-info)

[stackoverflow解决方法](https://stackoverflow.com/questions/750172/how-to-change-the-author-and-committer-name-and-e-mail-of-multiple-commits-in-gi?rq=1)

需要特别注意的是：

```
To change the name and/or email address recorded in existing commits, you must rewrite the entire history of your Git repository.

为了修改 commit 的作者邮箱地址，你必须重写整个 git 仓库历史。

Warning: This action is destructive to your repository's history. If you're collaborating on a repository with others, it's considered bad practice to rewrite published history. You should only do this in an emergency.

警告： 这个操作会破坏你的仓库历史， 如果你和别人在协同开发这个仓库，重写已发布的历史记录是一个不好的操作。建议只在紧急情况操作。
```

具体操作步骤如下：
* (1)打开终端
* (2)Create a fresh, bare clone of your repository: （新建一个全新的本地临时仓库信息：)

```
git clone --bare https://github.com/github用户名/仓库名.git
cd 仓库名.git
```

比如当前仓库地址为https://github.com/baohenglin/HLBlog.git

也就是：

```
git clone --bare https://github.com/baohenglin/HLBlog.git
cd HLBlog.git
```

* (3)Copy and paste the script, replacing the following variables based on the information you gathered: (复制以下脚本并将其粘贴到终端，并将以下的变量修改为你需要的)。

脚本如下：

```
#!/bin/sh

git filter-branch --env-filter '

OLD_EMAIL="your-old-email"
CORRECT_NAME="Your Correct Name"
CORRECT_EMAIL="your-correct-email"

if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```
需要修改的三个变量是OLD_EMAIL、CORRECT_NAME、CORRECT_EMAIL。

* (4)Press Enter to run the script.（按下 enter 键来运行这个脚本)
* (5)Review the new Git history for errors.(校对新的 git 仓库历史）
* (6)Push the corrected history to GitHub:（将修改后的仓库历史推到远程）

```
git push --force --tags origin 'refs/heads/*'
```
* (7)Clean up the temporary clone: (删除这个临时仓库)

```
cd ..
rm -rf 仓库名.git
//rm -rf HLBlog.git
```

## 5. git的基本命令

[⭐️⭐️⭐️⭐️⭐️Git使用详解](https://www.git-scm.com/book/zh/v2/Git-基础-远程仓库的使用)

(1)新建一个本地分支的同时切换到该分支：

```
git checkout -b 分支名称

```

(2)将新建的本地分支push到远程服务器:

```
git push origin 本地分支名称:远程分支名称
```

(3)查看本地分支：

```
git branch
```

(4)查看远程所有分支：

```
git branch -a
```

(5)切换到developBranch分支：

```
git checkout developBranch
```

(6)查看当前文件状态

```
git status
```
(7)将修改信息放到暂存区：

```
git add “修改的文件”
```

(8)将所有修改放到暂存区：

```
git add .
```

(9)提交

```
git commit -m 'commitMsg'
```

(10)查看尚未暂存的文件更新了哪些部分。git diff 本身只显示尚未暂存的改动，而不是自上次提交以来所做的所有改动。

```
git diff
```

(11)若要查看已暂存的将要添加到下次提交里的内容，可以用 git diff --cached 命令。Git 1.6.1 及更高版本还允许使用 “git diff --staged”

```
git diff --cached
```
(12)查看所有提交历史。

```
git log 
```

(13)查看最近两次的提交

```
git log -2
```

(14)详细打印最近5次的代码修改。此命令特别适用于进行代码审查。

```
git log -p -5
```

(14)查看Git当前的配置详情：

```
git config --list
```

(15)撤销工作空间的改动代码（撤销commit且撤销add）

```
git reset --hard HEAD^
```

(16)只撤销commit，不撤销git add，（不撤销工作空间的改动代码）

```
git reset --soft HEAD^
```

## 6.git push时报错“! [rejected]        master -> master (non-fast-forward)”的解决方法：

(1)把远程仓库和本地同步，消除差异。终端命令如下：

```
git pull origin master --allow-unrelated-histories 
```

(2)重新执行如下命令：

```
git add .
git commit -m '提交描述'
```

(3)重新push

```
git push origin master
```

# 7. 将本地代码文件上传到GitLab的终端命令

```
// Git global setup
git config --global user.name "baohenglin"
git config --global user.email "baohenglin@unioncast.cn"
```

```
// Push an existing folder
cd existing_folder
git init
git remote add origin http://192.168.101.107:82/app/ios/thepeopledaily.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

```
// Create a new repository
git clone http://192.168.101.107:82/app/ios/thepeopledaily.git
cd thepeopledaily
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

```
// Push an existing Git repository
cd existing_repo
git remote rename origin old-origin
git remote add origin http://192.168.101.107:82/app/ios/thepeopledaily.git
git push -u origin --all
git push -u origin --tags
```

# 8 如何设置Git的本地代理访问外网（通过外网访问 Git）

```
git config --global http.proxy 'http://user_name:password@http_proxy_ip:port'
//git config --global http.proxy 'http://zhangsan:abcd1234@192.168.20.1:8080'
```



