`Username`: fabiofeng3

`Password`: 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



# 仓库的创建和注册

```shell
#创建一个名为github的文件夹作为仓库
mkdir github
git init
#设置git用户名和邮箱
git config --local user.name fabiofeng3
git config --local user.email fabiofeng3@gmail.com
git config --global user.name fabiofeng3
git config --global user.email fabiofeng3@gmail.com
```

# 克隆仓库

```shell
git clone https://github.com/Gazler/cloneme    #将下载到当前目录下，且文件夹命名与网上的保持一致
git clone https://github.com/Gazler/cloneme my_cloned_repo
#仍然是下载到当前目录，但文件夹的名字为自己拟定的
```

# 使用git status指令查看当前仓库的状态

```shell
git status
```

![avatar](/home/f/文档/typora/git/status_en.png)

![avatar](/home/f/文档/typora/git/status_cn.png)

* 总体分为两个部分：tracked和untracked。而tracked又分为三个部分：modified and staged, modified but not staged, not modified。所以总共有1+3=4部分，其中tracked but not modified是隐藏的，因而在git status中最多显示三个分区。
* 一开始仓库文件夹里的所有文件都属于untracked分区，必须对文件执行`git add`指令后才能让其进入tracked三区（严格来说是进入tracked三区中的modified and staged分区）。所谓tracked，就是关注的意思，git将记住你add时文件的样子，一旦你对文件进行修改（包括物理删除，就是直接从硬盘里移除了），git将会检测到本地文件夹与系统暂存内容（staging area）的不同并进行提示，也就是将有更改的文件夹放入modified but not staged分区中。

# 修改仓库中的.gitignore文件

.gitignore文件的主要功能是你在使用`git add .`命令，将仓库文件夹的所有文件放入staging area时，系统将忽略那些在.gitignore有记录的文件。这么做的意义是可以忽略掉一些很大的文件，加快`git add .`的速度。

```shell
#.gitignore是一个隐藏文件，里面记录了git忽略文件的规则
vim .gitignore
#按i开始编辑，按esc退出编辑，输入:wq保存编辑内容并离开vim
#.gitignore是按照正则匹配工作的，打开以后应默认有如下内容
.profile.yml
.gitignore
#如果我们还想让git忽略所有以.swp为后缀的文件，就要在后面添加上
*.swp
#如果我们想要忽略所有以.a为后缀的文件，但单单不忽略lib.a这一文件，我们要添加
*.a
!lib.a
#！感叹号是说别忽略它
```





# 基础操作



## 提交文件

```shell
#提交单个文件
git add README
git commit -m "add README"
#其中git commit是对你本次作出的修改作注释罢了，是给别人看的

#提交仓库文件夹中的所有文件
git add .  #.就是当前文件夹的意思，..是上一级文件夹
```


## 将文件从staging area中删除

主要是从tracked area删除文件，分为两种情况：

* 从unstaged area中删除文件（changes not staged for commit）
* 从staged area中删除文件（changes to be commit）

### 从modified but not staged中删除文件

有一个文件从硬盘中删除了，但是并未从 git 仓库中删除，找到它并从 git 仓库中删除。删除也是修改的一种，提交这个修改就好了。

![avatar](/home/f/文档/typora/git/delete.png)

```shell
git add deleteme.rb   #相当于用空气覆盖掉了原来暂存的文件
git commit -m "remove deleteme.rb"
```

### 从modified and staged中删除文件

将一个新文件从 `staged area` 中删除。按照要求，不应该直接从硬盘上删除这个文件，只是从git中删除而已。加上 `--cache` 可以将文件只单纯从 `staged area` 中移除，不会真正的删除物理文件，如果要连这个物理文件也一起删除，请使用 `-f` 选项。

![avatar](delete2.png)

```shell
git rm --cached deleteme.rb   #由于硬盘中还有该文件，所以空气覆盖法不好使了，要换个指令
```





# 其它操作



## 用暂存区的版本覆盖本地版本（还原操作）

```shell
git stash   #可以恢复上次提交到本地
```

## 重命名文件

```shell
#第一种重命名是文件重命名
git mv oldfile.txt newfile.txt   #不仅会修改本地文件的名字，还会自动将重命名的文件添加到staging area

#第二种重命名中文件名并没有变化，是由于文件存储路径的改变而需要进行重命名
mkdir src
git mv *.html src
#创建了一个src文件夹，并将所有.html为后缀的文件放入其中
```

## 查看历史提交记录

```shell
git log   #可以查看最新commit的哈希值，提交时间和用户
```

## 为提交打标签tag

```shell
git tag new_tag   
#为最新的 commit 打 tag。不加额外参数就是为当前 commit 记录 tag, 当然可以为特定的 commit 打
```

## 将所有本地tag推送到远端

```shell
git push --tags origin master   #--tags 参数代表将所有的 tags 都推送到远端
```

