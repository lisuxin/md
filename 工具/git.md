将该文件夹变成Git可以管理的仓库：

```git
git init
```

然后通过git add将所有文件提交到暂存区：

```
git add .
```

add .是将所有文件提交 如果需要提交特定的文件 关于提交该项目特定的文件

```
通常会想到：git add [file1] [file2]   ；

这个方法添加文件比较慢，如果文件比较多怎么办？

 

git add *.扩展名

这条命令可以添加同类型的所有文件，是方便了不少；但是如果要添加不同类型文件怎么办？或者不完全add所有同类型文件怎么办？

git add -h: 帮助说明

 

接下来整理几个高级用法：（注意有个小数点）

git add .    ->这条命令可以探测到新增、修改、删除；应该比较常用；

 

git add -u .    -> u代表updata，你更新你已经跟踪的文件；如果你添加了新文件，那么你是不会主动跟踪，并提交的。所以这条明白无法探测新增文件；还是建议用上一条吧！这条命令还是有用的，如果你只是把一些你不想add的文件放在目录而已，那就用这条命令去add已经建立跟踪的文件。

 

git add -A .  包括了前两项
```

git commit -m '说明'提交到版本库中即可。

```
git commit -m 'the initial edition' //（'版本描述'）
```

需要将本地仓库与GitHub网站的仓库进行关联。

```
git remote add origin 
```

**git更换远程仓库地址**

**方法一**

```
git remote -v  #查看远端地址
git remote #查看远端仓库名
git remote set-url origin https://gitee.com/xx/xx.git (新地址)
```

**方法二**

```
git remote rm origin #删除远程的仓库
git remote add origin  https://gitee.com/xx/xx.git(新地址) #重新添加远程仓库
```

**方法三**

修改`.git`文件夹
`.git`文件夹一般在项目文件夹的第一层文件夹
`.git`文件在系统里默认是隐藏的，`windows`需要设置显示，`linux`使用`ls -a`查看

修改`config`文件内容，将[remote "origin"] `url` 修改成需要替换的`url`

**关联**

在将本地仓库与`GitHub`网站上的仓库进行关联后，便可进行推送了，但是在第一次进行推送时，需要注意的是，`GitHub`网站上的仓库并非是空的，我们在创建时创建了一个`README`文档，因此需要将两者进行合并才行。

```
git pull --rebase origin master
```

**在进行推送即可**

```
git push -u origin main
```

* 这个带有-u这个参数是指，将master分支的所有内容都提交，第一次关联之后后边你再提交就可以不用这个参数了，之后你的每一次修改，你就可以只将你修改push就好了。

```
git push origin master
```

