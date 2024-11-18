[TOC]

# Git

## 命令

**`git`兼容==所有的==`linux`命令**

## 创建用户 

| 命令 | 作用 |
| :--: | :--: |
| ` git config --global user.name ~~~~ ` | 初始化用户名 |
| `git config --global user.email ~~~~` | 初始化邮箱 |
| `git config user.name` | 查看用户名 |
| `git config user.email` | 查看邮箱 |
| `git config --list` | 查看配置信息 |
| `git config --global core.editor "code -w"` | 将`vsCode`设为默认编辑器 |

***配置文件在`C:\Users\rickey`下的`.gitconfig`中***

==只需要设置一次即可==

## 查看git版本

|      命令       |     作用      |
| :-------------: | :-----------: |
| `git --version` | 查看`git`版本 |

## 初始化本地库命令

| 命令 | 作用 |
| :--: | :--: |
| `git init` | 在当前目录下初始化本地库 |

## 查看本地库状态

|     命令     |      作用      |
| :----------: | :------------: |
| `git status` | 查看本地库状态 |

## git概念

- **工作区：**在电脑里能看到的目录
- **暂存区：**英文叫 stage 或 index。一般存放在 **.git** 目录下的 index 文件（.git/index）中，所以暂存区也叫作索引（index）
- **版本库：**工作区有一个隐藏目录 **.git**，这个不算工作区，而是 Git 的版本库

## 文件操作

### 将工作区文件添加至暂存区

|        命令        |           作用           |
| :----------------: | :----------------------: |
| `git add demo.txt` | 将`demo.txt`添加至暂存区 |

`git add *`或`git add .`: 将所有文件添加至暂存区

### 将暂存区的文件移除

|            命令            |           作用           |
| :------------------------: | :----------------------: |
| `git rm --cached demo.txt` | 将`demo.txt`从暂存区移除 |

### 将暂存区文件提交至本地库

|                命令                 |               作用               |
| :---------------------------------: | :------------------------------: |
| `git commit -m "日志信息" demo.txt` | 将`demo.txt`从暂存区提交至本地库 |

### 查看提交文件的版本

|          命令           |                             作用                             |
| :---------------------: | :----------------------------------------------------------: |
|        `git log`        |                  查看提交文件的详细版本信息                  |
|      `git reflog`       |                  查看提交文件的简略版本信息                  |
| `git log --graph --all` |   查看本地+远程所有分支的全部提交的详细版本信息的树形结构    |
|      `gitk --all`       | 查看本地+远程所有分支的全部提交的详细版本信息的树形结构==UI界面== |

### 版本回退

|            命令            |          作用           |
| :------------------------: | :---------------------: |
| `git reset --hard 0000000` | 将版本回退至`0000000`版 |

## 分支操作

1. **检查分支是否存在**：首先，确认本地仓库中是否有 `main` 分支。可以通过运行以下命令来查看：
   ```sh
   git branch
   ```
   如果列表中没有显示 `main` 分支，

2. **创建并切换到 main 分支**：如果 `main` 分支确实不存在，您可能需要从远程仓库中检出（check out）这个分支，或者如果您本意是要推送当前分支但名字不是 `main`，则应使用正确的分支名。首先，确保你知道远程仓库中的分支名称，然后可以创建并切换到 `main`（如果远程存在该分支）：
   ```sh
   git checkout -b main origin/main
   ```
   这条命令会从远程的 `main` 分支创建一个本地的 `main` 分支，并立即切换到该分支。

3. **设置跟踪信息**：如果之前没有设置过跟踪关系，可以按照一开始的提示操作，设置 `main` 分支跟踪远程的 `origin/main`：
   ```sh
   git branch --set-upstream-to=origin/main main
   ```

4. **再次尝试推送**：完成上述步骤后，你应该能够成功推送 `main` 分支到远程仓库了。
   ```sh
   git push -u origin main
   ```

### 创建分支

|         命令         |       作用        |
| :------------------: | :---------------: |
| `git branch hot-fix` | 创建分支`hot-fix` |

### 查看分支

|      命令       |     作用     |
| :-------------: | :----------: |
| `git branch` | 查看本地分支 |
| `git branch -v` | 查看本地分支详细信息 |
|`git branch -r`|查看远程分支|
|`git branch -a`|查看本地和远程分支|

### 切换分支

|          命令          |             作用              |
| :--------------------: | :---------------------------: |
| `git checkout hot-fix` | 将操作位置切换至`hot-fix`分支 |

### 合并分支

|        命令         |                           作用                            |
| :-----------------: | :-------------------------------------------------------: |
| `git merge hot-fix` | 将`hot-fix`分支合并至`master`主分支上（在主分支进行操作） |

#### 自动合并失败

原因：git无法判断修改的位置要如何取舍，需要手动合并

文件内容：

```txt
<<<<<<< HEAD
当前分支代码
=======
将被合并分支代码
>>>>>>> hot-fix <--将被合并分支的名称
```

==手动修改完成后同样需要手动添加和提交==

```shell
git add demo.txt
git commit -m "日志信息"
# 提交时不带文件名！
```

###  分支名修改

|            命令             |               作用               |
| :-------------------------: | :------------------------------: |
| `git branch -m master main` | 将`master`分支重命名为`main`分支 |

### 删除分支

|               命令                |                 作用                 |
| :-------------------------------: | :----------------------------------: |
|      `git branch -d master`       |         删除本地分支`master`         |
| `git push origin --delete master` | 删除远程库`origin`的远程分支`master` |

## 使用git本地库与远程库（GitHub）交互

### 将git连接至远程库（GitHub）

#### 查看远程库别名

|      命令       |              作用              |
| :-------------: | :----------------------------: |
| `git remote -v` | 查看当前目录下是否有远程库别名 |

#### 创建远程库别名

|                          命令                          |              作用               |
| :----------------------------------------------------: | :-----------------------------: |
| `git remote add nightMode https://github.com/~~~~.git` | 将远程库链接别名设为`nightMode` |

### 通过git上传和下载远程库（GitHub）内容

#### 将本地库文件推送至远程库

|            命令             |                            作用                             |
| :-------------------------: | :---------------------------------------------------------: |
| `git push nightMode master` | 将本地库的`master`分支推送至远程库`nightMode`的`master`分支 |

#### 将远程库文件下载至本地库

|            命令             |                            作用                             |
| :-------------------------: | :---------------------------------------------------------: |
| `git pull nightMode master` | 将远程库`nightMode`的`master`分支下载到本地库的`master`分支 |

#### 将远程库文件克隆至本地库

|                          命令                          |                         作用                          |
| :----------------------------------------------------: | :---------------------------------------------------: |
|        `git clone https://github.com/~~~~.git`         |            将远程库`nightMode`克隆到本地库            |
|   `git clone -b master https://github.com/~~~~.git`    | 将远程库`nightMode`的`master`分支克隆到本地库(文件夹) |
| `git clone -b master https://github.com/~~~~.git test` |  将远程库`nightMode`的`master`分支克隆到本地库`test`  |

> 克隆的特点
>
> 1. ==克隆不需要登陆账户==
> 2. 克隆会自动初始化本地仓库
> 3. 克隆会自动创建别名远程库的别名，默认为`origin`

## 配置git忽略文件

在`C:\Users\user`下创建文件`.gitignore`；在`C:\Users\user`下的`.gitconfig`中添加

```shell
[core]
	excludesfile = ~/.gitignore
```

> 例：防止git追踪.class文件
>
> ```shell
> *.class
> ```
>
> >所有通配符
> >
> >```shell
> ># 以斜杠“/”开头表示目录
> ># 以星号“*”通配多个字符
> ># 以问号“?”通配单个字符
> ># 以方括号“[]”包含单个字符的匹配列表
> ># 以叹号“!”表示不忽略(跟踪)匹配到的文件或目录
> >```

### 为单个`git`项目配置忽略文件

在`git`项目的与`.git`同级的目录下创建文件`.gitignore`，按照全局配置的方法进行配置忽略即可

# Github

## 创建远程库

1. 点击右上角加号，选择`New repository`
2. 在`Repository name`中输入创建的仓库名，点击创建
3. 在创建完成的仓库中点击`Code`，复制`HTTPS`下的远程库链接

### *远程库特殊命名*

建立一个与自己`GitHub`账户同名的仓库，并勾选`README`后，只需要修改`README`文件就可以美化个人主页

## 添加成员（团队内合作）

### 添加方

1. 点击远程库的`Settings`按钮
2. 点击`Manage access`按钮
3. 点击`Invite a collaborator`，输入被添加方的github名称并确认
4. 点击被被添加方旁的邀请链接代码（`Pending Invite`）发送给被添加方

### 被添加方

1. 进入添加方发来的邀请链接代码点击`Accept invitation`

## 跨团队合作

### 非团队成员

1. 搜索到需要合作的项目
2. 点击右上角`Fork`将代码叉到自己的代码库进行开发
3. 修改完成后点击远程库的`Pull requests`按钮，再点击`New pull request`按钮
4. 点击`Create pull request `按钮，输入注释再提交

### 团队内成员

1. 点击远程库的`Pull requests`按钮
2. 确认非团队成员代码无误后点击`Merge pull request`再点击`Confirm merge`进行合并

## 使用SSH免密登录

### 生成ssh密钥

**生成的密钥在`C:\Users\user\.ssh`中**

> **私钥：**<kbd>`id_rsa`</kbd>
>
> **公钥：**<kbd>`id_rsa.pub`</kbd>

```shell
cd C:\Users\user\
ssh-keygen -t rsa -C y
# 输入生成密钥命令后按三次回车
# ssh-keygen --> 生成ssh密钥的命令
# -t rsa --> 使用rsa加密算法
# -C --> 加密GitHub邮箱
```

### 添加ssh密钥

1. 点击`Github`头像选择`Settings`
2. 选择`SSH and GPG keys`，点击`New SSH key`
3. 输入当前公钥的名字（自定义）和公钥，点击`Add SSH key`

### 使用ssh密钥

**推送和下载时直接操作即可**

# GIT

### 版本控制

```
版本迭代
版本控制是一种在开发的过程中用于管理我们对文件、目录或工程等内容的修改历史，方便查看和更改历史记录，备份以便恢复以前版本的软件工程技术。
```

+ 实现跨区域多人协同给开发

+ 追踪和记载一个或多个文件的历史记录
+ 组织和保护你的源代码和文档
+ 统计工作量
+ 并行开发、提高效率
+ 跟踪记录整个软件的开发过程
+ 减轻开发人员的负担，节省时间，同时降低人为错误

**常见的版本控制工具**

`GIT`、`SVN`、`CVS`、`VSS`、`TFS`

影响力最大且使用最广泛的是`GIT`

### 版本控制分类

1. **本地版本控制**

   记录文件每次的更新，可以对每个版本做一个快照，或是记录补丁文件，适合个人用，如RCS

2. **集中版本控制**

   所有版本数据都保存在服务器上，协同开发者从服务器上同步跟新或上传自己的修该

3. **分布式版本控制**

   所有版本信息厂库全部同步到本地的每个用户

### GIT环境配置

```
git卸載
先刪除环境变量
安装.exe版本的直接无脑下一步
```

**启动Git**

鼠标右键

**Git Bash** : Unix 和 Linux 风格的命令行，使用最多

**Git CMD** : Windows 风格的命令行

**Git GUI** : 图形界面的git

### 常用Linux命令

```
cd:           改变目录
cd..          回到上一个目录，直接cd进入默认目录
pwd:          显示当前所在目录路径
ls(ll):       列出当前目录所有文件
touch:        新建文件
rm:           删除文件
mkdir:        新建目录
rm -r:        删除文件
mv            移动文件夹
reset         重新初始化终端/清屏
clear         清屏
history       查看命令历史
help          帮助
exit          退出
#             表示注释
```

# 提交基本步骤

将该文件夹变成Git可以管理的仓库：

```git
git init
```

然后通过git add将所有文件提交到暂存区：

```
git add .
```

`add .`是将所有文件提交 如果需要提交特定的文件 关于提交该项目特定的文件：git add用法

1. 通常会想到：git add [file1] [file2]   ；这个方法添加文件比较慢，如果文件比较多怎么办？
2. git add *.扩展名：这条命令可以添加同类型的所有文件，是方便了不少；但是如果要添加不同类型文件怎么办？或者不完全add所有同类型文件怎么办？
3. git add -h: 帮助说明 
   * 接下来整理几个高级用法：（注意有个小数点）
   * git add .    ->这条命令可以探测到新增、修改、删除；应该比较常用；
   * git add -u .    -> u代表updata，你更新你已经跟踪的文件；如果你添加了新文件，那么你是不会主动跟踪，并提交的。所以这条明白无法探测新增文件；还是建议用上一条吧！这条命令还是有用的，如果你只是把一些你不想add的文件放在目录而已，那就用这条命令去add已经建立跟踪的文件。 
   * git add -A .  包括了前两项

### git的username和email

1. 查看

   ```
   git config --global user.name
   git config --global user.email
   git config --list               //查看git的
   ```

2. 修改

   ```
   $ git config --global user.name  "name"//自定义用户名
   $ git config --global user.email "youxiang@qq.com"//用户邮箱
   ```

3. git使用的username和email

   ```
   lisuxin
   18582969757@189.cn
   ```

### git提交错误退回提交状态

1. 打开github(仓库)，找到历史提交(Commits)复制提交分支id

2. 使用命令回退到指定提交

   ```
   git reset --hard 提交id
   ```

3. 强制推送到仓库

   ```
   git push origin 分支 --force
   ```

### git更换远程仓库地址

**方法一**

1. `git remote -v`  #查看远端地址
2. `git remote` #查看远端仓库名
3. `git remote set-url origin https://gitee.com/xx/xx.git` (新地址)

**方法二**

1. `git remote rm origin` #删除远程的仓库
2. `git remote add origin  https://gitee.com/xx/xx.git`(新地址) #重新添加远程仓库

**方法三**

1. 修改`.git`文件夹
2. `.git`文件夹一般在项目文件夹的第一层文件夹
3. `.git`文件在系统里默认是隐藏的，`windows`需要设置显示，`linux`使用`ls -a`查看
4. 修改`config`文件内容，将[remote "origin"] `url` 修改成需要替换的`url`

**关联**

1. 在将本地仓库与`GitHub`网站上的仓库进行关联后，便可进行推送了，但是在第一次进行推送时，需要注意的是，`GitHub`网站上的仓库并非是空的，我们在创建时创建了一个`README`文档，因此需要将两者进行合并才行。

   ```
   git pull --rebase origin master
   ```

2. 需要将本地仓库与GitHub网站的仓库进行关联。

   ```
   git remote add origin 
   ```

**在进行推送即可**

* 这个带有-u这个参数是指，将master分支的所有内容都提交，第一次关联之后后边你再提交就可以不用这个参数了，之后你的每一次修改，你就可以只将你修改push就好了。

   ```
   git push -u origin main
   git push origin master
   ```

# 代码提交

## 方法一

1. 拉取代码`git clone 厂库地址`

2. 提交代码到暂存区`git add .`

3. 添加注释信息`git commit -m '提交信息'`

4. 将代码提交`git push -u origin master`


## 方法二

1. 创建本地版本库,创建文件夹`mkdir 文件夹名`

2. 把文件夹变成Git可管理的厂库`git init`

3. 添加项目到厂库`git add .   //git status查看当前状态`

4. 查看已经add的`git status`

5. 消除本地与远程仓库之间的异差`:q!强制退出vim、git pull origin main `
6. 添加注释提交`git commit -m '注释信息'`

7. 创建SSH KEY`ssh-keygen -t rsa -C "地址" //不做修改一直回车`



# 新项目提交步骤

1. `git init`：把文件夹变成Git可管理的厂库
2. `git remote add origin 地址`：绑定远程仓库
3. `git add .`：提交到暂存区
4. `git commit -m ''`：信息
5. `git branch -m master main `：修改分支main分支
6. `git push -u origin main`提交
7. 后续项目正常提交步骤

# 报错

## git branch后出现* (no branch, rebasing main)

当你在Git中执行 `git branch` 命令后看到输出中有 `* (no branch, rebasing main)`，这表示你当前处于一个特殊的状态，即你正在进行或已经中断了对 `main` 分支的变基操作（rebase）。

这里有几个关键点：
- ***(no branch)***：这表明当前工作区没有关联到任何明确命名的分支上。通常，当你检出一个特定分支时，Git会告诉你当前正处于哪个分支，但在这个情形下，因为你在进行变基，Git暂时将你置于一个无名的分支状态。

- **rebase main**：这意味着你之前执行了类似 `git rebase main` 的命令，尝试将你当前的工作（可能是一个特性分支）基于 `main` 分支的最新状态进行重新定位。变基操作会暂停你的工作流，逐个应用你在当前分支上所做的提交，放到 `main` 分支的最新提交之上。

解决或继续这个过程，你可以根据情况选择以下操作之一：

1. **继续变基**：如果你准备好继续并解决任何可能的冲突，可以使用 `git rebase --continue` 命令。Git会尝试应用下一个待处理的提交。如果有冲突，你需要先解决冲突，然后才能继续。

2. **放弃变基**：如果你决定不再进行变基或者遇到了难以解决的问题，可以使用 `git rebase --abort` 命令来取消整个变基操作，这会回滚到变基开始前的状态。

3. **检查冲突**：如果存在冲突，Git会在发生冲突的文件中标记出来，你需要手动编辑这些文件，解决冲突，然后才能继续变基。

