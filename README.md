# git笔记
参考资料：https://www.liaoxuefeng.com/wiki/896043488029600


## 一、Git安装配置
1. Git简介
Git是目前世界上最先进的分布式版本控制系统。
    

2. Git安装
下载Git： https://gitforwindows.org/

安装：图形化界面安装，可直接选择默认选项，安装即可；

3. 配置
安装完成后，每个机器都必须自报家门，配置如下：

```
$ git config --global user.name  "Your Name"

$ git config --global user.email  "email@example.com"
```
 

## 二、创建Git版本库

### 1.  创建仓库目录

```
$ mkdir learngit

$ cd learngit

$ pwd
```

### 2. 初始化，使得文件夹为仓库

```
$ git init
```

### 3. 创建文件
如  建立readme.txt文件，内容如下（最好用notepad）：

```
Git is a version control system.

Git is free software.
```

### 4. 添加

```
$ git add readme.txt
```

### 5. 提交

```
$ git commit -m "wrote a readme file"
```

##  三、远程仓库
 
### 0. 注册github账号，创建仓库
注册github账号，免费获得Git远程仓库。 注册账号和创建仓库比较简单，此处略。

### 1. 创建SSH Key
为保证GitHub仓库 “认识” 你的电脑，需要创建SSH Key。

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```
， 然后一路回车，即可生成秘钥。

在用户主目录下的.ssh目录(Windows系统下为 C:\Users\userName\.ssh)，生成 id_rsa和id_rsa.pub这两个文件。id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

### 2. 在gitHub上添加公钥
登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“SSH and GPG keys”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容即可。

### 3. 测试是否成功
在本地建立文件夹，在该文件夹下运行：

```
git clone git@github.com:usrer/repos.git ;     
```

git@github.com:usrer/repos.git 为gitHub仓库地址，仓库成功拷贝下来。


##  四、本地仓库与远程仓库
 

### 1. 创建本地仓库
可见  创建Git版本仓库 。

### 2. 创建Github上的仓库
创建Github上的仓库 为图形化界面操作，此处略。（注意，创建仓库的时候不要勾选Initialize this repository with a README）。

### 3. 关联本地仓库与Github上的远程仓库

```
git remote add origin git@github.com:username/reponame.git 
```

命令中username  为Github用户名，reponame为Github仓库名。

### 4. 推送本地仓库内容到远程仓库

```
git push -u origin master
```

-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

### 5. 其他
5.1 如果出现错误： fatal: remote origin already exists.
解决办法如下：

```
$ git remote rm origin
```

5.2 直接克隆远程仓库到本地电脑

```
git clone git@github.com:username/reponame.git
```

命令中username  为Github用户名，reponame为Github仓库名。

5.3 其他有关远程仓库命令
查看远程仓库 ：

```
git remote -v 或git remote
```

删除远程仓库origin标签 ：

```
git remote rm origin 或者 git remote remove  origin 
```

添加一个远程库的标签：

```
git remote add gitlab git@gitlab.com:abc/blog.git
```

推送到gitlab标签：

```
git push gitlab master
```

修改origin标签对应的地址：

```
git remote set-url origin git@gitlab.com:abc/blog.git
```

把gitlab 标签改名为coding： 

```
git remote rename gitlab coding
```





##  五、分支管理
 
Git分支是由指针管理起来的，所以创建、切换、合并、删除分支都非常快，非常适合大型项目的开发。在分支上做开发，调试好后再合并到主分支，那么每个人开发模块式都不会影响到别人。
Git分支相关命令如下：

```
查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b <name>

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>

推送本地分支(feature1)到远程仓库：git push origin feature1
查看推送后的结果： git branch -a

删除远程分支：git push origin --delete feature1



```


### 1、分支合并实例1 


```
（1）修改本分支（master分支）内容并提交

原feature1.txt 中内容为：
new content

修改为:
 new content master 


添加并提交：
$ git add feature1.txt 
$ git commit -m "add master modify"
 
（2）准备新的feature1分支并切换：

$ git checkout -b feature1


原feature1.txt最后一行，改为：
修改为 new content feature1

 
（3）在feature1分支上提交：
$ git add feature1.txt 
$ git commit -m "add feature1 modify"


（4）切换到master分支：
$ git checkout master
 
（5）尝试合并
$ git merge feature1

命令行出现以下错误：
 
Auto-merging feature1.txt
CONFLICT (content): Merge conflict in feature1.txt
Automatic merge failed; fix conflicts and then commit the result.
 
 表示同时修改了feature1.txt，出现了冲突。

可用 $ git status  查看状态提示

（6）打开冲突的文件查看冲突

<<<<<<< HEAD

new content master
 
=======
new content feature1
>>>>>>> feature1


以上错误的说明：
<<<<<<< HEAD

本地代码

=======

拉下来的代码

>>>>>>>

（7）修改冲突的文件
修改feature1.txt为：
new content  merge

提交修改：

$ git add feature1.txt 
$ git commit -m "modify conflict"
 

（8）用带参数的git log也可以看到分支的合并情况：
$ git log --graph --pretty=oneline --abbrev-commit


```
 


### 2、分支合并实例2


```
 (0) 远程仓库feature1.txt 的master分支修改:

原feature1.txt 中内容为：
new content merge 

修改为：
new content merge remote

提交：
$ git add feature1.txt 
$ git commit -m "add remote"


（1）修改本分支（master分支）内容并提交

原feature1.txt 中内容为：
new content 

修改为:
new content merge local


添加并提交：
$ git add feature1.txt 
$ git commit -m "add local"

（2） 拉取代码

$ git pull origin master

发生冲突：

From github.com:qinpmc/gitlearn
 * branch            master     -> FETCH_HEAD
Auto-merging feature1.txt
CONFLICT (content): Merge conflict in feature1.txt
Automatic merge failed; fix conflicts and then commit the result.

（3）查看冲突文件

打开 feature1.txt ：
<<<<<<< HEAD
new content  merge local
=======
new content  merge remote
>>>>>>> 5d1929407d795ea3bc0003625ef4a1557f4c82d6


（4） 解决冲突提交
修改冲突的 feature1.txt 为：
new content  merge 2



### 3、分支实例3


```
Bug分支

（1）当前正在dev分支工作，且进行的工作还没有提交：

不是不想提交，而是工作只进行到一半，还没法提交，
接到一个修复一个代号101的bug的任务时，想创建一个分支issue-101来修复它



（2）把当前工作现场“储藏”起来，等以后恢复现场后继续工作
$ git stash


（3）假定需要在master分支上修复，就从master创建临时分支：
$ git checkout master

$ git checkout -b issue-101



（4）在分支issue-101修复bug，然后提交：

$ git add readme.txt 
$ git commit -m "fix bug 101"


（5）修复完成后，切换到master分支，完成合并，最后删除issue-101分支：

$ git checkout master

$ git merge --no-ff -m "merged bug fix 101" issue-101

$ git branch -d issue-101


（6）回到dev分支干活
$ git checkout dev

$ git stash list  --查看工作现场

（7）恢复工作现场，有两个办法

a）git stash apply恢复，但恢复后stash内容并不删除,需要用git stash drop来删除；

b)git stash pop，恢复的同时把stash内容也删去：


（8）查看工作现场
$ git stash list  --查看工作现场，此时无stash

 


```





```

## 六、版本回退

1. 历史记录查看 git log：

```
$ git log
$ git log --pretty=oneline    或$ git log --oneline

```

2. git reflog用来记录你的每一次命令：

```
 ---查找commit id
$ git reflog
```
3. 版本回退

在Git中，用HEAD表示当前版本，也就是最新的提交3628164...882e1e0，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

```
$ git reset --hard HEAD^     //回退到上一次提交


$ git reset --hard 3628164    
注：3628164 为版本id ，版本号没必要写全，前几位就可以了，Git会自动去找

```
 

4. 撤销

（1）场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

```
$ git checkout -- readme.txt
```

（2）场景2：当你不但改乱了工作区某个文件的内容，还添加（git add）到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。

```
$ git reset HEAD readme.txt
$ git checkout -- readme.txt

```

（3）场景3：已经提交（git commit）了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

```
$ git reset --hard 3628164

```
 
## 七、标签管理
 
标签管理相对比较简单，主要涉及以下几个命令：

```
1. 查看所有标签：git tag
2. 创建标签 : git tag tagname 
3. 指定提交信息 : git tag -a name -m "comment"
4. 删除标签 : git tag -d tagname
5. 标签发布到远程仓库 : git push origin tagname
6. 删除远程标签：git push origin :refs/tags/tagname
7. 忘了给以前的版本打标签:
    git log --pretty=oneline --abbrev-commit
    git tag v0.9 6224937        //6224937 为提交id
    // git tag -a v0.1 -m "version 0.1 released" 3628164   //带评论的tag
8. 查看标签信息： git show v0.9
```


## 八、git仓库忽略文件及指定仓库语言
 
1 、自定义git仓库语言
git 仓库会自动根据提交的文件判断仓库的语言，但有时不太准确，可以自定义修改,
仓库中新建  .gitattributes 文件，文件内容大致如下：

```
# Auto detect text files and perform LF normalization
# 本示例将.html .js 文件均视作js语言
*.js linguist-language=javascript
*.html linguist-language=javascript
```

2 、 git仓库忽略文件

- （1）. 仓库中新建  .gitignore文件，文件内容大致如下：

```
# 忽略node_modules 文件夹
node_modules

# Windows:
Thumbs.db
ehthumbs.db
Desktop.ini

# Python:
*.py[cod]
*.so
*.egg

# Java:
*.class
```

- （2）. 此时无法添加 .class 文件 ，git status 无法查看到该文件

- （3）. 确实想添加该文件，可以用-f强制添加到Git：

```
git add -f App.class

```
 


## 九、配置别名

- （1）用st表示status：

```
$ git config --global alias.st status
```

- (2)用unstage表示reset HEAD

```
$ git config --global alias.unstage 'reset HEAD'
```

- (3)用last表示最近一次提交（命令中无--global

```
$ git config  alias.last 'log -1'
```

- （4）加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用    
  
  
- (5) 每个仓库的Git配置文件都放在.git/config文件中：

```
$ cat .git/config 
```

别名就在[alias]后面，要删除别名，直接把对应的行删掉即可。

- (6) 而当前用户的Git配置文件放在用户主目录（/c/Users/userName/）下的一个隐藏文件.gitconfig中：

```
$ cat .gitconfig
```


## 十、其他

- 1. 有时git 命令行文件目录为数字形式的目录，处理方式：

```
git config --global core.quotepath false
```






















