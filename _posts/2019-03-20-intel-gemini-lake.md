---
layout: blog
title: 英特尔 Gemini Lake 处理器
---

## {{page.title}}

-----------------------
[Gemini Lake]{:target="_blank"} 是 Intel 于 2017 年下半年推出的，在此之前 Intel 在低功耗移动平台上的主力还是 14nm 工艺的 [Apollo Lake]{:target="_blank"}、[Braswell] 处理器。

[Gemini Lake]{:target="_blank"} 维持在 14nm 工艺，架构从 [Apollo Lake] 的 Goldmont 小升级为 Goldmont Plus，L2 缓存也从 2MB 升级到 4MB，提升执行效率和性能；GPU 部份使用 Gen9LP 引擎（HD605、HD600），依然是支撑 4K 60Hz 分辨率的输出，內建 HDMI 2.0 控制器，提供 VP9 10bit Profile2 硬件解码。除了显示部份提升外，支持蓝牙 5 和 无线 802.11ac Wave 2 2x2 160MH。CPU 最多4核，TDP 功耗移动版 6W、桌面版 10W。

内存最高支持 DDR4/LPDDR4-2400、双通道、最大 8 GB。显卡支持 eDP/DP/HDMI/MIPI-DSI 接口、4K 60Hz。

|型号|发布|内核数<br>线程数|TDP|基本<br>频率|脉冲<br>频率|缓存|显卡型号|执行<br>单元|显卡频率<br>MHz
|:---:|:---:|:---:|---:|:---:|:---:|:---:|:---:|:---:|:---
|奔腾 [J5005]{:target="_blank"}|Q4'17|4/4|10W|1.5GHz|2.8GHz|4MB|HD 605|18|250-800
|赛扬 [J4105]{:target="_blank"}|Q4'17|4/4|10W|1.5GHz|2.5GHz|4MB|HD 600|12|250-750
|赛扬 [J4005]{:target="_blank"}|Q4'17|2/2|10W|2.0GHz|2.7GHz|4MB|HD 600|12|250-700
|
|奔腾 [N5000]{:target="_blank"}|Q4'17|4/4|6W|1.1GHz|2.7GHz|4MB|HD 605|18|200-750
|赛扬 [N4100]{:target="_blank"}|Q4'17|4/4|6W|1.1GHz|2.4GHz|4MB|HD 600|12|200-700
|赛扬 [N4000]{:target="_blank"}|Q4'17|2/2|6W|1.1GHz|2.6GHz|4MB|HD 600|12|200-650
{:style="min-width:40em"}

> 英特尔 CPU 发布时间 Q4`17 指的是 2017 年的第四季度，Q = quarter 季度。


[Gemini Lake]: https://ark.intel.com/content/www/cn/zh/ark/products/codename/83915/gemini-lake.html "去官网查看"
[Apollo Lake]: http://ark.intel.com/zh-cn/products/codename/80644/Apollo-Lake "去官网查看"
[Braswell]: http://ark.intel.com/products/codename/66094/Braswell#@All "去官网查看"

[J5005]: https://ark.intel.com/content/www/cn/zh/ark/products/128984/intel-pentium-silver-j5005-processor-4m-cache-up-to-2-80-ghz.html "去官网查看"
[J4105]: https://ark.intel.com/content/www/cn/zh/ark/products/128989/intel-celeron-j4105-processor-4m-cache-up-to-2-50-ghz.html "去官网查看"
[J4005]: https://ark.intel.com/content/www/cn/zh/ark/products/128992/intel-celeron-j4005-processor-4m-cache-up-to-2-70-ghz.html "去官网查看"

[N5000]: https://ark.intel.com/content/www/cn/zh/ark/products/128990/intel-pentium-silver-n5000-processor-4m-cache-up-to-2-70-ghz.html "去官网查看"
[N4100]: https://ark.intel.com/content/www/cn/zh/ark/products/128983/intel-celeron-n4100-processor-4m-cache-up-to-2-40-ghz.html "去官网查看"
[N4000]: https://ark.intel.com/content/www/cn/zh/ark/products/128988/intel-celeron-n4000-processor-4m-cache-up-to-2-60-ghz.html "去官网查看"


### 相关阅读：

- [英特尔 Apollo Lake 处理器]({{ '/2017/03/01/intel-apollo-lake.html' | prepend: site.github.url }}) - 2017-03-01
- [英特尔 Braswell 处理器]({{ '/2016/03/15/intel-braswell.html' | prepend: site.github.url }}) - 2016-03-15


[Gemini Lake 正式加入產品線，Intel 發表新款 Pentium Silver 與 Celeron 處理器]: https://www.techbang.com/posts/55680-gemini-lake-formally-joins-the-product-line-intel-publishes-the-new-pentium-silver-and-celeron-processor
[Apollo Lake继任者：英特尔Gemini Lake处理器芯片曝光]: https://www.ithome.com/html/digi/273414.htm
[Intel Gemini Lake处理器曝光：性能提升巨大]: http://www.d1net.com/chip/market/494272.html
[Intel 14nm低功耗Gemini Lake架构曝光：全能SoC]: https://news.mydrivers.com/1/544/544595.htm