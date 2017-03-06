---
layout: blog
title: 英特尔 Apollo Lake 处理器
---

## {{page.title}}

-----------------------
[Apollo Lake]{:target="_blank"} 是 Intel 于 2016 年下半年推出的，在此之前 Intel 在低功耗移动平台上的主力还是 14nm 工艺的 [Braswell]{:target="_blank"}、Cherry Trail 处理器。

[Apollo Lake]{:target="_blank"} 维持在 14nm 工艺，架构从现有的 Airmont 更换为 Goldmont，提升执行效率和性能；GPU 部份使用全新的 Gen9 引擎（HD500、HD505），支撑 4K 分辨率的输出。除了显示部份提升外，在 I/O 方面，Goldmont 架构的 Apollo Lake 开始全面支撑 Type-C 以及 eMMC 5.0。 Apollo Lake SoC 封装为 FCBVGA 1296 type 3，Z-height 为 1.5mm。可以把 Goldmont 看作桌面版 Skylake 架构的精简版，CPU 最多4核。TDP 功耗 6.5W 到 12W。

内存最高支持 DDR3L/LPDDR3-1866、LPDDR4-2400、双通道、最大 8 GB。显卡支持 eDP/DP/HDMI/MIPI-DSI。

|型号|发布|内核数<br>线程数|TDP|基本<br>频率|脉冲<br>频率|缓存|显卡型号|执行<br>单元|显卡频率<br>MHz
|:---:|:---:|:---:|---:|:---:|:---:|:---:|:---:|:---:|:---
|奔腾 [J4205]{:target="_blank"}| |4/4|10W|1.5GHz|2.6GHz|2MB|HD 505|18|250-800
|赛扬 [J3455]{:target="_blank"}|Q3'16|4/4|10W|1.5GHz|2.3GHz|2MB|HD 500|12|250-750
|赛扬 [J3355]{:target="_blank"}|Q3'16|2/2|10W|2.0GHz|2.5GHz|2MB|HD 500|12|250-700
|
|奔腾 [N4200]{:target="_blank"}|Q3'16|4/4|6W|1.1GHz|2.5GHz|2MB L2|HD 505|18|200-750
|赛扬 [N3450]{:target="_blank"}|Q3'16|4/4|6W|1.1GHz|2.2GHz|2MB L2|HD 500|12|200-700
|赛扬 [N3350]{:target="_blank"}|Q3'16|2/2|6W|1.1GHz|2.4GHz|2MB L2|HD 500|12|200-650
|
|凌动 [x7-E3950]{:target="_blank"}|Q4'16|4/4|12W|1.6GHz|2.0GHz|2MB L2|HD 505|18|500-650
|凌动 [x7-E3940]{:target="_blank"}|Q4'16|4/4|9.5W|1.6GHz|1.8GHz|2MB L2|HD 500|12|400-600
|凌动 [x7-E3930]{:target="_blank"}|Q4'16|2/2|6.5W|1.3GHz|1.8GHz|2MB L2|HD 500|12|400-550
{:style="min-width:40em"}

注：英特尔 CPU 发布时间 Q3`16 指的是 2016 年的第三季度，Q = quarter 季度。


[Braswell]: http://ark.intel.com/products/codename/66094/Braswell#@All "去官网查看"
[Apollo Lake]: http://ark.intel.com/zh-cn/products/codename/80644/Apollo-Lake "去官网查看"

[J4205]: http://ark.intel.com/zh-cn/products/95591/Intel-Pentium-Processor-J4205-2M-Cache-up-to-2_6-GHz "去官网查看"
[J3455]: http://ark.intel.com/zh-cn/products/95594/Intel-Celeron-Processor-J3455-2M-Cache-up-to-2_3-GHz "去官网查看"
[J3355]: http://ark.intel.com/zh-cn/products/95597/Intel-Celeron-Processor-J3355-2M-Cache-up-to-2_5-GHz "去官网查看"

[N4200]: http://ark.intel.com/zh-cn/products/95592/Intel-Pentium-Processor-N4200-2M-Cache-up-to-2_5-GHz "去官网查看"
[N3350]: http://ark.intel.com/zh-cn/products/95598/Intel-Celeron-Processor-N3350-2M-Cache-up-to-2_4-GHz "去官网查看"
[N3450]: http://ark.intel.com/zh-cn/products/95596/Intel-Celeron-Processor-N3450-2M-Cache-up-to-2_2-GHz "去官网查看"

[x7-E3950]: http://ark.intel.com/zh-cn/products/96488/Intel-Atom-x7-E3950-Processor-2M-Cache-up-to-2_00-GHz "去官网查看"
[x7-E3940]: http://ark.intel.com/zh-cn/products/96485/Intel-Atom-x5-E3940-Processor-2M-Cache-up-to-1_80-GHz "去官网查看"
[x7-E3930]: http://ark.intel.com/zh-cn/products/96486/Intel-Atom-x5-E3930-Processor-2M-Cache-up-to-1_80-GHz "去官网查看"


### 相关阅读：

- [英特尔 Braswell 处理器]({{ '/2016/03/15/intel-braswell.html' | prepend: site.github.url }}) - 2016-03-15


[Intel下半年推Apollo Lake平台：优化功耗，将成本降到底]: http://www.expreview.com/46649.html
[Intel发新一代Atom：性能暴涨190％ 110°C下保用15年]: http://news.mydrivers.com/1/504/504834.htm