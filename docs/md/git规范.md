# Git 规范

### 👉 通用设置

为了方便追踪代码的开发者或修改者，需要以真实姓名进行提交代码，

可以运行以下命令进行设置：

```
git config --global user.name "自己的真实姓名"  

git config --global user.email "自己的邮箱"
```

:::note 注意

`--global` 参数是全局设置，对所有项目生效。

:::

可以运行以下命令查看当前设置的姓名和邮箱等信息：

```
git config --list

```

### 👉 提交流程

##### 1、拉取代码

即将仓库里的代码更新到本地（新建一个位于文件夹位置的终端窗口进行操作）

```
git pull origin master
```

##### 2、提交本次更新的目录

```
git add .
```

##### 3、说明本次修改了什么

```
git commit -m ‘添加了新内容’
```

##### 4、提交更新

```
git push origin master
```

### 👉 本地预览

本地预览自己更改的效果。

本地预览常用地址（根据每个项目而定）：[http://localhost:3000](http://localhost:3000) 或者 [http://localhost:8000](http://localhost:8000)

```
yarn start
```

