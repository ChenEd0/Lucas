# Git 常用命令

## 常用

#### 区分文件名称大小写

默认情况下git是忽略区分大小写的，多人合作的情况下不规范很容易造成问题，所以开启区分大小写。

**开启**

```
git config core.ignorecase false
```

**查看**

查看是否修改完毕，找到 core.ignorecase=false 即说明修改完毕。

```
git config --list
```

#### 查看本地所有分支

```
git branch
```

#### 查看当前状态

```
git status
```

#### 查看远程所有分支

```
git branch -r
```

#### 切换本地分支

v2 即本地的另一个分支名称。

```
git checkout v2
```

#### 查看提交日志

```
git log
```

#### 清除提交缓存区

cached 其实就是暂存区，然后一个是工作的目录，你的工作目录的东西做出修改时，会和缓存区进行对比，因此你 git status 时，会显示出来这个差异，因此为了使 `.gitignore` 中的内容生效，那么就删除掉暂存区，然后将所有本地文件追踪一下，就得到最新的暂存区文件。

```
git rm -r --cached .
```

## 提交命令

#### 提交本次更新的目录

```
git add .
```

#### 说明本次修改了什么

```
git commit -m ‘添加了新内容’
```

#### 提交更新

master 是仓库的分支名称。

```
git push origin master
```

### 
