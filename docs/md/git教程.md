# Git 教程

### 👉 克隆现有的仓库

右键新建目标文件夹的终端，然后复制粘贴以下的命令。

```
git clone https://github.com/xxxx/test.git
```

### 👉 创建一个新的仓库

##### 1、在仓库新建一个 README.md 文件

```
echo "# test" >> README.md 
```

##### 2、git 初始化

```
git init
```

##### 3、提交 README.md 文件到版本更改列表

```
git add README.md
```

##### 4、提交版本更改说明

```
git commit -m "first commit"
```

##### 5、将分支更改为 main

```
git branch -M main
```

##### 6、添加远程仓库的地址

```
git remote add origin https://github.com/xxxx/test.git
```

##### 7、提交到仓库的 main 分支

```
git push -u origin main
```



### 👉 推送现有的仓库

##### 1、添加远程仓库的地址

```
git remote add origin https://github.com/xxxx/test.git
```

##### 2、将分支更改为 main

```
git branch -M main
```

##### 3、提交到仓库的 main 分支

```
git push -u origin main
```



### 👉 从另一个仓库导入代码

可以使用Subversion、Mercurial或TFS项目中的代码初始化此存储库。
