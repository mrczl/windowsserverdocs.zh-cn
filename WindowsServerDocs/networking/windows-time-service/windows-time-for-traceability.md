---
ms.assetid: ''
title: Windows 时间实现可追溯性
description: 许多行业的法规都要求系统可追溯到 UTC。  这意味着可以根据 UTC 证明系统的偏移量。
author: shortpatti
ms.author: dacuo
manager: dougkim
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 307739042426088fa92c50e6ea4dc5d2a744f15a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405204"
---
# <a name="windows-time-for-traceability"></a>Windows 时间实现可追溯性
>适用于：Windows Server 2016 版本 1709 或更高版本，以及 Windows 10 版本 1703 或更高版本


许多行业的法规都要求系统可追溯到 UTC。  这意味着可以根据 UTC 证明系统的偏移量。  为启用法规合规性方案，Windows 10（版本 1703 或更高版本）和 Windows Server 2016（版本 1709 或更高版本）需提供新的事件日志，以提供操作系统方面的信息，便于了解对系统时钟执行的操作。  这些事件日志会为 Windows 时间服务持续生成，并且可以进行检查或存档以便进行后续分析。

这些新的事件有助于回答以下问题：

* 是否更改了系统时钟
* 是否修改了时钟频率
* 是否修改了 Windows 时间服务配置

## <a name="availability"></a>可用性

这些改进添加在 Windows 10 版本 1703 或更高版本以及 Windows Server 2016 版本 1709 或更高版本中。

## <a name="configuration"></a>配置

无需进行任何配置即可实现此功能。  默认情况下，这些事件日志处于启用状态，并且可在 Applications and Services Log\Microsoft\Windows\Time-Service\Operational 路径下的事件查看器中找到  。


## <a name="list-of-event-logs"></a>事件日志列表

下节概述记录的用于可追溯性方案的事件。

# <a name="257tab257"></a>[257](#tab/257)
Windows 时间服务 (W32Time) 启动时会记录此事件，并记录关于当前时间、当前滴答计数、运行时配置、时间提供程序和当前时钟速率的信息。

|||
|---|---|
|事件描述 |服务启动 |
|详细信息 |启动 W32time 时发生 |
|记录的数据 |<ul><li>当前 UTC 时间</li><li>当前滴答计数</li><li>W32Time 配置</li><li>时间提供程序配置</li><li>时钟速率</li></ul> |
|限制机制  |无。 每次启动服务时都会触发此事件。 |

**示例：**
```
W32time service has started at 2018-02-27T04:25:17.156Z (UTC), System Tick Count 3132937.
```

**命令：**

还可以使用以下命令查询此信息

W32Time 和时间提供程序配置 
```
w32tm.exe /query /configuration
```

时钟速率 
```
w32tm.exe /query /status /verbose
```


# <a name="258tab258"></a>[258](#tab/258)
Windows 时间服务 (W32Time) 停止时会记录此事件，并记录关于当前时间和滴答计数的信息。

|||
|---|---|
|事件描述 |服务停止 |
|详细信息 |关闭 W32time 时发生 |
|记录的数据 |<ul><li>当前 UTC 时间</li><li>当前滴答计数</li></ul> |
|限制机制  |无。 每次停止服务时都会触发此事件。 |

示例文本：  
`W32time service is stopping at 2018-03-01T05:42:13.944Z (UTC), System Tick Count 6370250.`

# <a name="259tab259"></a>[259](#tab/259)
此事件定期记录时间源和所选时间源的当前列表。  此外，它还会记录当前滴答计数。  每次更改时间源时不会触发此事件。  本文档后面列出的其他事件提供此功能。

|||
|---|---|
|事件描述 |NTP 客户端提供程序定期状态 |
|详细信息 |NTP 客户端使用的时间源列表 |
|记录的数据 |<ul><li>可用的时间源</li><li>记录日志时所选的参考时间服务器</li><li>当前滴答计数</li></ul>  |
|限制机制  |每 8 小时记录一次。 |

示例文本：  NTP 客户端提供程序定期状态：

NTP 客户端正在接收来自以下 NTP 服务器的时间数据：

server1.fabrikam.com,0x8 (ntp.m|0x8|[::]:123->[IPAddress]:123)server2.fabrikam.com,0x8 (ntp.m|0x8|[::]:123->[IPAddress]:123)；所选的参考时间服务器为 Server1.fabrikam.com,0x8 (ntp.m|0x8|[::]:123->[IPAddress]:123) (RefID:0x08d6648e63)。 系统滴答计数为 13187937

命令  还可以使用以下命令查询此信息

标识对等
`w32tm.exe /query /peers` 

# <a name="260tab260"></a>[260](#tab/260)

|||
|---|---|
|事件描述 |时间服务配置和状态 |
|详细信息 |W32time 定期记录其配置和状态。 这等效于调用：<br><br>`w32tm /query /configuration /verbose`<br>或者<br>`w32tm /query /status /verbose` |
|限制机制  |每 8 小时记录一次。 |

# <a name="261tab261"></a>[261](#tab/261)
使用 SetSystemTime API 修改系统时间时，它会记录每个实例。

|||
|---|---|
|事件描述 |已设置系统时间 |
|限制机制  |无。<br><br>时间同步合理的系统上应很少出现此情况，我们希望在每次出现此情况时对其进行记录。 我们在记录此事件时会忽略 TimeJumpAuditOffset 设置，因为该设置用于限制 Windows 系统事件日志中的事件。 |

# <a name="262tab262"></a>[262](#tab/262)

|||
|---|---|
|事件描述 |已调整系统时钟频率 |
|详细信息 |当时钟处于紧密同步状态时，W32time 会持续修改系统时钟频率。 我们希望捕获对时钟频率做出的“相当重要的”调整，而无需过度运行事件日志。 |
|限制机制  |不会记录低于 TimeAdjustmentAuditThreshold（最小值 = 128 PPM，默认值 = 800 PPM）的所有时钟调整。<br><br>在当前粒度下，2 PPM 的时钟频率变化会导致出现 120 µsec/sec 的时钟准确度变化。<br><br>在同步系统上，大部分调整都低于此级别。 如果要细化跟踪信息，则可以向下调整此设置或使用 PerfCounters，也可以同时执行这两个操作。 |

# <a name="263tab263"></a>[263](#tab/263)

|||
|---|---|
|事件描述 |更改时间服务设置或列出已加载的时间提供程序。 |
|详细信息 |重新读取 W32time 设置会导致在内存中修改某些关键设置，这可能会影响时间同步的整体准确性。<br><br>W32time 会在重新读取其设置时记录每个事件，这些事件会对时间同步产生潜在影响。 |
|限制机制  |无。<br><br>仅当管理员或 GP 更新更改时间提供程序并触发 W32time 时，才会发生此事件。 我们希望记录每个更改设置的实例。 |


# <a name="264tab264"></a>[264](#tab/264)

|||
|---|---|
|事件描述 |更改 NTP 客户端使用的时间源 |
|详细信息 |当时间服务器/对等机更改状态（挂起 -> 同步、同步 -> 无法访问或其他转换）时，NTP 客户端会记录包含时间服务器/对等机最新状态的事件   |
|限制机制  |最高频率 - 仅每 5 分钟一次，以保护日志不受临时问题和不良提供程序实现的影响。 |

# <a name="265tab265"></a>[265](#tab/265)

|||
|---|---|
|事件描述 |时间服务源或分层编号更改 |
|详细信息 |W32time 时间源和分层编号是时间可追溯性中的重要因素，必须记录对其做出的任何更改。 如果 W32time 没有时间源，且未配置为可靠的时间源，则它将停止作为时间服务器进行播发，并根据设计使用一些无效参数来响应请求。 此事件对于跟踪 NTP 拓扑的状态更改至关重要。 |
|限制机制  |无。 |


# <a name="266tab266"></a>[266](#tab/266)

|||
|---|---|
|事件描述 |请求重新同步时间 |
|详细信息 |此操作在以下情况下触发：<ul><li>发生网络更改时</li><li>系统从连接的待机/休眠状态返回</li><li>长时间未同步</li><li>管理员发出重新同步命令</li></ul>此操作会立即导致丢失细粒度的时间同步准确度，因为它会使 NTP 客户端清除筛选器。 |
|限制机制  |最高频率 - 每 5 分钟一次。<br><br>错误的网卡（或不良脚本）可能会重复触发此操作，并造成日志过多。 因此需要限制此事件。<br><br>请注意，准确的时间同步需要 5 分钟以上的时间才能完成，并且限制不会丢失导致时间不准确的原始事件的相关信息。  |

---
