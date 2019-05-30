
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
