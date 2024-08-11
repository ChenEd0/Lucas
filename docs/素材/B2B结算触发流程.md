---
title: B2B结算触发流程
description: B2B结算触发流程
sidebar_position: 3
last_update:
  author: 罗润华
---

>:palm_tree:**<big>一、平台结算（以账期结算为例）</big>**

    1、平台后台的会员支付策略中的（以线下支付为例，会员在测试过程中的支付方式选择线下支付线上确认）“资金收集模式”设置为“平台代收模式”

![](@site/static/img/test_img/2022-08-11-15-08-23.png)
![](@site/static/img/test_img/2022-08-11-15-09-58.png)

    2、平台后台：系统-平台规则-平台结算策略设置-设置账期X天（X代表，支付成功后X天后进入平台结算）

![](@site/static/img/test_img/2022-08-11-15-28-34.png)

    3、B2B采购商发起采购（跑完付款即可）（支付方式记得选择为线下支付线上确认哦，然后去平台后台-待确认支付结果订单中点击确认）


    4、打开navicat：找到对应环境的数据库下ord_payment表，若第二步设置了账期X天，然后将对应数据行的confirm_time字段改成X天前的时间（如：设置了账期1天，则将对应数据行的confirm_time字段改成一天前得任意时间即可）,记得保存哦。

![](@site/static/img/test_img/2022-08-11-19-29-04.png)

    5、打开postman跑一下数据，URL填入对应环境的接口网管+report/feign/platformSettlement

![](@site/static/img/test_img/2022-08-11-19-29-15.png)

    6、最后可到服务提供者-能力中心-结算-平台结算管理-平台代收账款页面&平台后台-平台结算-代收账款结算中进行数据查看了

![](@site/static/img/test_img/2022-08-11-19-30-51.png)

![](@site/static/img/test_img/2022-08-11-19-31-08.png)

![](@site/static/img/test_img/2022-08-11-19-34-50.png)

:::tip 提示
测试前需按照当前会员角色清空对应表中内容sa_platform_settlement、sa_platform_settlement_detail，否则调用接口时无法产生
:::

>🐳**<big>二、会员结算（以月结为例）</big>**

    1、服务提供者的能力中心-结算-结算规则配置-会员策略配置中设置（如：月结X号，由于代码层面原因，假如今天是X号就只能设置X号）

![](@site/static/img/test_img/2022-08-11-19-45-48.png)

    2、B2B采购商发起采购（跑完付款即可）（支付方式记得选择月结X号（名字来源服务提供者的能力中心设置那个名字））

    3、打开navicat：找到对应环境的数据库下ord_payment表，然后将对应数据行的paytime_time字段改成上个月任意时间,记得保存哦。

    4、打开postman跑一下数据，URL填入对应环境的接口网关+report/feign/memberSettlement

![](@site/static/img/test_img/2022-08-11-20-08-28.png)

    5、最后可到服务提供者、服务消费者-能力中心-结算-应收账款管理页面中进行数据查看了

![](@site/static/img/test_img/2022-08-11-20-07-51.png)

![](@site/static/img/test_img/2022-08-11-20-07-00.png)

:::tip 提示
测试前需按照当前会员角色清空对应表中内容sa_member_order_settlement、sa_member_settlement，否则调用接口时无法产生
:::