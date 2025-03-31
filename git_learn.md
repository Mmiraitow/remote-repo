#### 目的：

要学会基本的操作，满足面试以及真正工作的需求

包括但不限于：下载仓库 本地修改 同步 提交等 还有版本控制

使用方式：命令行 GUI IDE插件/拓展

git config命令配置用户名和邮箱----才能识别出来是谁提交的内容

git bash是？  **windows上的终端模拟器**，提供类似于Linux的命令行环境（基于Mintty和MSYS2），cmd和powershell对unix命令支持有限

启动文件夹是？

默认编辑器  怎么还有编辑器



#### 初始化

git config --global user.name chaoyang

git config --global user.email 18864493159@163.com

git config --global credential.helper store

git config --global --list   //查看全局配置



#### 新建版本库（仓库） 

管理本地代码

理解成一个目录

创建仓库  将一个目录变成git管理的仓库

**git init** //从电脑本地直接创建      git init +名称  在当前目录再创建一个新的目录做仓库

**git clone** //从远程服务器克隆已经存在的仓库

//需要先创建一个目录

.git是个隐藏目录，需要ls -a才能查看  ls看不到  隐藏起来是因为里面的东西不能随意动

删除.git  仓库会消失，即当前目录将不再是一个git仓库了

.git目录存放了git仓库的所有数据

ls -altr是什么？ a：所有all   l:long 长格式  t：time按时间修改顺序  r：反向排序



#### 区域和文件位置

工作区（.git所在目录）实际操作的目录

暂存区(.git/index):临时存储 用于保存即将提交到git仓库的修改内容

本地仓库(.git/objects)  就是git_init创建的仓库

在工作区修改后 **git add** 到 暂存区 ，暂存区 **git commit** 到本地仓库

可以git add多次后再统一git commit到仓库

**git commit到仓库中后才算真正被保管起来，其只会提交暂存区中的文件**



**文件状态：**

未跟踪  未被git管理

未修改  被管理但未改变

已修改 已修改但未git add

已暂存  已git add

git status 查看状态

git rm --cached file1.txt    //从暂存区移除

**echo "second file" > file2.txt**   新建一个文件及其内容，unix应该同样

**通配符批量操作：git add *.txt**，添加所有txt结尾的文件

​			   **git add . 将当前文件夹下的所有文件add**



git log查看提交记录 每次提交都有一个唯一的id   

git log --oneline 简洁的提交记录



#### 回退版本

**HEAD指向该分支的最新提交节点**

**git reset + 要回退的版本ID**，回到之前的某一个提交状态（HEAD指针的指向）  HEAD^表示回退到上一个版本

git reset --soft 工作区和暂存区的**修改内容**都保留，只是变成了新内容，修改后再暂存+提交就是了

git reset --hard 都不保留 **真的要放弃所有修改内容时使用，慎用**  但是也可以回溯，找到版本号即可

git reset --mixed （默认）只保留工作区 丢弃暂存区



**ls查看工作区的内容，其实就是你的本地文件，就是你的本地工作区**

**git ls-files查看暂存区的内容，但其实是所有已经被跟踪的文件，应该包括加入暂存区和提交的**



#### git diff 查看差异

- **比较本地仓库、工作区、暂存区之间的差异**

默认比较工作区与暂存区（哪些内容为被添加到暂存区）

工作区与版本库(仓库)  git diff HEAD

暂存区与版本库  git diff --cached

- **不同版本的差异**

  git diff + 两次提交的版本id

  **git HEAD~ HEAD/git HEAD^ HEAD,比较上一个与当前**git HEAD~i HEAD 表示比较HEAD之前的i个版本

  再+文件名 就只会查看该文件的差异内容

- **不同分支的差异**

直接+两个分支的名称



#### 从版本库删除文件

删除仓库方法一：从工作区删除后，暂存区还没删除，git add .   在此时就是从暂存区删除 （更新暂存区）,再提交

方法二： git rm  工作区（本地）和暂存区都会删，**删除后记得提交，否则版本库中还存在，上同**

git rm --cached 只删除暂存区，不删除本地（删完记得提交），即该文件不再被跟踪

#### .gitignore

不应被加入到版本库中的文件

**遵循原则：**

​	系统或工具自动生成的文件，

​	编译产生的中间文件和结果文件(.o)

​	日志文件，缓存文件 ，临时文件

​	涉及身份、密码、token的敏感信息文件

将文件添加到.gitignore文件中，echo access.log > .gitignore

git add.  **将所有修改都添加到暂存区**     *.log匹配所有以log为结尾的文件

先前被加入到版本库中的文件是没办法被忽略的，还是能被追踪

忽略文件夹：temp/   文件夹的形式是以/为结尾的

git默认不添加空的文件夹

**匹配规则：**

使用标准的glob模式匹配，即简化的正则表达式：

​	*通配任意个字符

​	？匹配单个字符

​	[]

​	**表示匹配任意的中间目录

​	[0-9]表示任意一位数字  [a-z]表示任意一位小写字母

​	！表示取反     ！+目录表示忽略此目录以外的其他目录

​	/TODO表示当前目录下的TODO文件



#### 远程仓库

GitHub

SSH  需要配置密钥   而HTTP则需要用户名和密码  这里推荐前者

在./ssh目录生成SSH密钥  **ssh-keygen -t rsa -b 4096**

id_rsa为密钥文件

id_rsa(私钥文件，谁也不给)  id_rsa.pub（公钥文件，上传到GitHub）





第一次配置都是默认的   而且密码也没有设置

再想配置就需要再起名字，不然会覆盖

且还要多一些配置：创建config文件 ：访问GitHub时指定密钥

tail -5 config   后面用到再说



远程和本地怎么关联起来的？？ 我克隆别人的 修改后能 git push吗？？ 感觉跟前面的SSH有关



**先git clone克隆到本地修改，修改完再git push提交到远程仓库**



git push git pull :同步本地和远程

<img src="D:\ysp_development\屏幕截图 2025-03-13 173111.png" style="zoom:80%;" />



##### 添加远程仓库   仓库要先在远程建好，可以同时关联多个远程仓库

**git remote add  + 远程仓库别名 + 远程仓库地址**           添加远程仓库（应该是通过本地仓库进行）

git push -u origin main:main   关联本地仓库与该远程仓库，并将本地的main分支推送给远程仓库的main分支

**这里的main要改成master，版本问题**



**拉取远程仓库的(修改)内容**

git pull + 远程仓库别名 + 要拉取的分支     会自动做一次合并操作，无冲突则会合并成功

git fetch  只获取修改，不会自动合并到本地仓库，需要手动合并



gitlab：可以私有化部署 



#### 分支 branch

**git branch + 分支名，创建一个新的分支**

**git checkout + 分支名， 切换到该分支**        **但是git checkout + 文件名还表示回退文件，如果分支名和文件名相同会存在歧义，且默认是转换分支**

**git switch 专门用来切换分支**



**git merge dev           合并分支,     dev表示将要被合并的分支**   分支被合并并不会消失

git branch -d dev  删除已经完成合并的分支（只能删除已合并的） -D是强制删除



#### 解决合并分支的冲突

两个分支的修改内容重合了（同一个文件的同一行代码）

**git commit -a = git add + git commit**

提交肯定是提交到当前分支嘛

如何解决：手工编辑，留下想要的内容后再提交 commit

也可以在合并中 git merge --abort终止合并



#### Rebase 变基 合并分支   相当于嫁接移植

可以在任意分支上使用rebase      merge一般在main/master分支上

**每个分支都有一个指针，指向当前分支的最新提交记录**

**从分叉点把整个分支都移动到目标分支的最新提交记录后面**

**git rebase**

cp 复制文件夹



**git rebase 与 git merge**

merge不会破坏原分支的提交历史，方便回溯和查看，但会产生额外的提交节点，分支图比较复杂

rebase 不会新增额外的提交记录，形成线性历史，比较直观和干净，会改变提交历史，**需要避免在共享分支上使用**





#### 工作流模型 GitFlow      GitHubFlow

pull request  PR（MR）  合并请求   CR没问题后再合并

tag 版本号   每次合并都要有

