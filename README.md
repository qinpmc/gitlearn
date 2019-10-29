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
```



















