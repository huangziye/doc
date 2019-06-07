
# 初次运行 Git 前的配置

```
# 设置用户名
git config --global user.name "用户名"

# 设置邮箱
git config --global user.email "邮箱"

# 查看 git 配置信息
git config --list

# 查看用户名
git config --global user.name

# 查看邮箱
git config --global user.email

# 查看当前使用的 git 目录
which git
```

> --global 表示全局配置，如果是针对某个项目进行单独的配置，可以使用 --system


# 初始化仓库

```
git init
```

# 克隆仓库

```
git clone [url]

git clone [url] 自定义本地仓库的名字
```


# 添加文件


```
git add [file]
```


# 提交文件

```
git commit -m "commit message" [file]
```

# 查看当前文件的状态

```
git status

# 状态简览
git status -s 或 git status --short
```

# 查看历史记录

```
git log

# 以一行显示每次提交的log
git log --pretty=oneline 或 git log --oneline

git reflog
# 其中 HEAD@{移动到当前版本需要多少步}
```
> 对于多屏显示时，空格向下翻页，b向上翻页，q退出


# 版本前进/回退

```
git reset --hard [索引值]
```

# 删除文件并找回

前提：删除前，文件存在时的状态提交到了本地库。

操作：`git reset --hard [指针位置]`
> 删除操作已经提交到本地库：指针位置指向历史记录
>
> 删除操作尚未提交到本地库：指针位置使用HEAD 


# 比较文件差异

```
git diff
```
> 比较多个文件


```
git diff [文件名]
```
> 将工作区中的文件和暂存区进行比较

```
git diff [本地库中历史版本] [文件名]
```
> 将工作区中的文件和本地库历史记录比较




















# 创建分支

```
git branch <branchname>
```
不指定参数直接执行 `branch` 命令的话，可以显示分支列表。 前面有 `*` 的就是现在的分支。

```
git branch

或

git branch -v
```

# 切换分支

```
git checkout <branchname>
```

在 `checkout` 命令指定 `-b` 选项执行，可以创建分支并进行切换。

```
git checkout -b <branchname>
```


# 合并分支


执行merge命令以合并分支。

```
git merge <branchname>
```

该命令将指定分支导入到 `HEAD` 指定的分支。先切换 `master` 分支，然后把 `xxx` 分支导入到 `master` 分支。



# 删除分支

```
git branch -d <branchname>
```

# 更新远程数据库内容到本地



```
git pull
```

# fetch

执行 `pull`，远程数据库的内容就会自动合并。但是，有时只是想确认本地数据库的内容而不想合并。这种情况下，请使用 `fetch`。



# 从本地数据库 `push` 到远程数据库

```
git push
```



# 标签

Git 可以使用2种标签：`轻标签` 和 `注解标签`。打上的标签是固定的，不能像分支那样可以移动位置。

## 添加轻标签

```
git tag <tagname>
```

如果没有使用参数而执行 `tag`，可以显示标签列表。

```
git tag
```


如果在 `log` 命令添加 `--decorate` 选项执行，可以显示包含标签资料的历史记录。


```
git log --decorate
```


## 添加注解标签

若要添加注解标签，可以在 `tag` 命令指定 `-a` 选项执行。执行后会启动编辑区，请输入注解，也可以指定 `-m` 选项来添加注解。


```
git tag -a <tagname>

git tag -am [注解信息] [标签名]
```


如果在 `tag` 命令指定 `-n` 选项执行，可以显示标签的列表和注解。

```
git tag -n
```


## 删除标签

若要删除标签，在 `tag` 命令指定 `-d` 选项执行。

```
git tag -d <tagname>
```

# 改写提交

## 修改最近的提交

指定 `amend` 选项执行提交的话，可以修改同一个分支最近的提交内容和注解。

主要使用的场合：

- 添加最近提交时漏掉的档案
- 修改最近提交的注解


## 取消过去的提交

在 `revert` 可以取消指定的提交内容。使用后面要提到的 `rebase -i` 或 `reset` 也可以删除提交。
但是，不能随便删除已经发布的提交，这时需要通过 `revert` 创建要否定的提交。

主要使用的场合：

- 安全地取消过去发布的提交


## 遗弃提交

在 `reset` 可以遗弃不再使用的提交。执行遗弃时，需要根据影响的范围而指定不同的模式，可以指定是否复原索引或工作树的内容。


除了默认的 `mixed` 模式，还有 `soft` 和 `hard` 模式。欲了解受各模式影响的部分，请参照下面的表格。


| 模式名称 | HEAD的位置 | 索引 | 工作树 |
| --- | --- | --- | --- |
| soft | 修改 | 不修改 | 不修改 |
| mixed | 修改 | 修改 | 不修改 |
| hard | 修改 | 修改 | 修改 |

主要使用的场合：

- 复原修改过的索引的状态(mixed)
- 彻底取消最近的提交(hard)
- 只取消提交(soft)


## 提取提交

在 `cherry-pick`，您可以从其他分支复制指定的提交，然后导入到现在的分支。

主要使用的场合：

- 把弄错分支的提交移动到正确的地方
- 把其他分支的提交添加到现在的分支


## 改写提交的历史记录

在 `rebase` 指定i选项，您可以改写、替换、删除或合并提交。


主要使用的场合：

- 在push之前，重新输入正确的提交注解
- 清楚地汇合内容含义相同的提交。
- 添加最近提交时漏掉的档案


## 汇合分支上的提交，然后一同合并到分支

我们介绍一下 `merge` 的特殊选项：`squash`

用这个选项指定分支的合并，就可以把所有汇合的提交添加到分支上。

主要使用的场合：

- 汇合主题分支的提交，然后合并提交到目标分支。






