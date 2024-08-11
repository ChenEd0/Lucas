---
title: win11修改host
description: host修改
sidebar_position: 2
last_update:
  author: 郑学贤
---
# host修改

## 1、hosts文件位置

:::info 提示

首先找到hosts文件，W11的host文件目录是：`c:\windows\system32\drivers\etc`。

:::

![](@site/static/img/test_img/2022-07-19-10-54-07.png)

## 2、修改hosts文件权限

:::info 提示

选中hosts文件，右键选择属性，弹出属性窗口。

默认权限是只读状态，取消勾选。

:::

![](@site/static/img/test_img/2022-07-19-10-55-20.png)

:::info 提示

选择安全，点击编辑

:::

![](@site/static/img/test_img/2022-07-19-10-55-58.png)

:::info 提示

在权限允许栏，勾选允许修改以及读写

:::

![](@site/static/img/test_img/2022-07-19-10-56-33.png)

:::info 提示

点击确定。

:::
    
![](@site/static/img/test_img/2022-07-19-10-57-14.png)

:::info 提示

点击确定后，会弹出一个安全提示窗口，这个是正常现象，点击是。最后点击确定，完成hosts文件权限的修改

:::
    
![](@site/static/img/test_img/2022-07-19-10-57-51.png)

## 3、用记事本打开hosts文件修改

:::info 提示

搜索记事本，右键记事本，选择用管理员的身份运行，打开hosts文件，修改后保存。

:::

## 4、将hosts权限重新修改成只读

:::info 提示

将hosts权限重新改为只读，是出于电脑安全考虑。建议修改hosts之后一定不要漏了这个步骤

:::
