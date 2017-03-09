---
layout: blog
title: 迷你 PC 配置 - 华擎 Apollo Lake SoC ITX 主板
---

{{page.title}}
========

Apollo Lake 是 Intel 于 2016 年下半年推出的，华擎的主板跟得最快了。下面两套迷你 PC 配置，使用[华擎集成 Intel Apollo Lake CPU 的 ITX 主板](http://www.asrock.com/mb/index.asp?s=Intel%20CPU#Intel CPU){:target="_blank"}，特点还是迷你机箱、省电、省电、省电，CPU 的 TDP 功耗仅为 10W，用功率计实测主机功耗 20W 左右。

这两套配置应付日常上网、办公、看高清电影、玩小游戏绝对绰绰有余。主板还提供 DVI、VGA、HDMI、USB3 等丰富接口。
实测装 Win10 企业版，开机时间十几秒！

### 配置 1

这套配置是帮照仔老表的老婆配的，用于代替残旧龟慢的老办公电脑。听说老板很吝啬，不肯升级办公电脑，受不了龟慢的速度就自己买部替来用，有这样的员工老板真幸福。这个配置直接配了 Apollo Lake CPU 中性能最高的奔腾 J4205，4 核 4 线程，频率 1.5GHz~2.6GHz，集成显卡为 HD 505，18 个执行单元。

| | 配件 | 规格 | 单价 | 数量 | 备注
|---|---|:---:|---:|:---
| 1 | 主板 | 华擎 [J4205-ITX]{:target="_blank"} | [¥799][P1S1]{:target="_blank"} | 1 | 集成 CPU、网卡、声卡、显卡
| 2 | CPU | [J4205]{:target="_blank"} | | 1 | 14nm 4核4线程 1.5GHz-2.6GHz
| 3 | 内存 | 金士顿 4GB | [¥199][P1S3]{:target="_blank"} | 2 | DDR3L-1600 1.35v
| 4 | 硬盘 | 威刚 SP920 128GB | [¥389][P1S4]{:target="_blank"} | 1 | SATA3
| 5 | 机箱电源 | 立人 E-N3 标配 60W | [¥263][P1S5]{:target="_blank"} | 1 | 标配 LR1108 150W 直插电源及 12V5A 60W 适配器
| 6 | WIFI+蓝牙卡 | Intel 8260NGW | [¥99][P1S6]{:target="_blank"} | 1 | M.2 Key-E 2230 接口
| 7 | WIFI 转接线 | 外牙内针 | [¥8][P1S7]{:target="_blank"} | 2 | NGFF 网卡转 SMA 天线转接线
| 8 | WIFI 外置天线 | 内牙内孔 | [¥6][P1S8]{:target="_blank"} | 2 | 6DBi 全向高增益
| | | 合计 | ¥1976 | | 未配键鼠

注：点击单价可以跳转到购买链接，价格是 2017 年 2 月下旬查询得到的。

![E-N3]({{ site.github.url }}/images/mini-pc/20170227-E-N3-J3455-ITX.jpg){:style="max-width:98%"}

### 配置 2

这套配置是帮我弟弟配的，用于上网、看电影、常规 Office 文档处理，弟弟说最重要的是要打开很多个网页（上淘宝、京东）也不能慢。这个配置配了 Apollo Lake 桌面版 CPU 中性能排第 2 的赛扬 J3455，4 核 4 线程，频率 1.5GHz~2.3GHz，集成显卡为 HD 500，12 个执行单元。

| | 配件 | 规格 | 单价 | 数量 | 备注
|---|---|:---:|---:|:---
| 1 | 主板 | 华擎 [J3455-ITX]{:target="_blank"} | [¥559][P2S1]{:target="_blank"} | 1 | 集成 CPU、网卡、声卡、显卡
| 2 | CPU | [J3455]{:target="_blank"} | | 1 | 14nm 4核4线程 1.5GHz-2.3GHz
| 3 | 内存 | 金士顿 8GB | [¥389][P2S3]{:target="_blank"} | 1 | DDR3L-1600 1.35v
| 4 | 硬盘 | 威刚 SP920 128GB | [¥389][P2S4]{:target="_blank"} | 1 | SATA3
| 5 | 机箱电源 | 立人 E-W80 标配 60W | [¥265][P2S5]{:target="_blank"} | 1 | 标配 LR1204 120W 电源模块及 12V/5A 60W 适配器
| 6 | WIFI+蓝牙卡 | Intel 3168NGW | [¥46][P2S6]{:target="_blank"} | 1 | M.2 Key-E 2230 接口
| 7 | WIFI 转接线 | 外牙内针 | [¥5][P2S7]{:target="_blank"} | 2 | NGFF 网卡 IPX4 代转 SMA 线
| 8 | WIFI 外置天线 | 内牙内孔 | [¥4.5][P2S8]{:target="_blank"} | 2 | 原装TP-LINK 路由器双频 SMA 天线
| 9 | 无线键鼠 | 罗技 MK245 | [¥94][P2S9]{:target="_blank"} | 1 | NANO 小接收器
| | | 合计 | ¥1761

注：点击单价可以跳转到购买链接，价格是 2017 年 2 月下旬查询得到的。

![E-W80]({{ site.github.url }}/images/mini-pc/20170227-E-W80-J4205-ITX.jpg){:style="max-width:98%"}

### 性能测试

测试软件统一使用鲁大师 v5.15.16.1080 版。

| 配置 | 综合性能得分 | 处理器性能 | 显卡性能 | 内存性能 | 磁盘性能
|---|:---|:---|:---|:---|:---
| J4205-ITX_4Gx2_128G-SSD | 67637 ↑45% | 28140 ↑23% | 9257 ↑228% | 6720 | 8700
| J3455-ITX_8Gx1_128G-SSD | 57618 ↑23% | 25558 ↑11% | 5693 ↑102% | 6387 | 8430
| Q2900-ITX_4Gx2_128G-SSD | 46801      | 22927      | 2819       | 6528 | 7380

注：其中 Q2900-ITX 为 2014 年自用组装的迷你 PC，配置点 [这里]({{ site.github.url }}/2014/12/08/my-mini-pc.html)，CPU 为早期的 Bay Trail-D [J2900]。

![J4205-vs-J3455-vs-J2900]({{ site.github.url }}/images/lu/20170227-J4205-vs-J3455-vs-J2900.jpg){:style="max-width:98%"}


[J4205-ITX]: http://www.asrock.com/mb/Intel/J4205-ITX "去官网查看"
[J3455-ITX]: http://www.asrock.com.cn/mb/Intel/J3455-ITX/ "去官网查看"
[J4205]: http://ark.intel.com/zh-cn/products/95591/Intel-Pentium-Processor-J4205-2M-Cache-up-to-2_6-GHz "去官网查看"
[J3455]: http://ark.intel.com/zh-cn/products/95594/Intel-Celeron-Processor-J3455-2M-Cache-up-to-2_3-GHz "去官网查看"

[P1S1]: https://detail.tmall.com/item.htm?id=542215848173 "去天猫买"
[P1S3]: https://detail.tmall.com/item.htm?id=543653854649 "去天猫买"
[P1S4]: https://detail.tmall.com/item.htm?id=38492221936 "去天猫买"
[P1S5]: https://detail.tmall.com/item.htm?id=38538721713 "去天猫买"
[P1S6]: https://detail.tmall.com/item.htm?id=523153769123 "去天猫买"
[P1S7]: https://detail.tmall.com/item.htm?id=525299969278 "去天猫买"
[P1S8]: https://detail.tmall.com/item.htm?id=530885212185 "去天猫买"

[P2S1]: https://detail.tmall.com/item.htm?id=543864963216 "去天猫买"
[P2S3]: https://detail.tmall.com/item.htm?id=543620612867 "去天猫买"
[P2S4]: https://detail.tmall.com/item.htm?id=38492221936 "去天猫买"
[P2S5]: https://item.taobao.com/item.htm?id=27380468733 "去淘宝买"
[P2S6]: https://item.taobao.com/item.htm?id=543345752998 "去淘宝买"
[P2S7]: https://item.taobao.com/item.htm?id=532829952843 "去淘宝买"
[P2S8]: https://item.taobao.com/item.htm?id=530366708327 "去淘宝买"
[P2S9]: https://item.taobao.com/item.htm?id=18997006180 "去淘宝买"


*[SoC]: System on Chip
[J2900]: http://ark.intel.com/zh-cn/products/78868/Intel-Pentium-Processor-J2900-2M-Cache-up-to-2_67-GHz "去官网查看"
