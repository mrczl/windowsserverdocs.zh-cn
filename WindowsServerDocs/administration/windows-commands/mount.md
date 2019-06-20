---
title: 装载
description: 'Windows 命令主题 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dd9d7ecb-ef00-4aaa-bcd0-423fa636e34a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65083ce4b7d04129ff630a7f314c458d7ee378f4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437245"
---
# <a name="mount"></a>装载



可以使用**装载**以装载网络文件系统 (NFS) 网络共享。

## <a name="syntax"></a>语法

```
mount [-o <Option>[...]] [-u:<UserName>] [-p:{<Password> | *}] {\\<ComputerName>\<ShareName> | <ComputerName>:/<ShareName>} {<DeviceName> | *}
```

## <a name="description"></a>描述

**装载**命令行实用程序装载文件系统由标识*ShareName*导出的 NFS 服务器由标识*ComputerName*并将其与通过指定的驱动器号*DeviceName*或者，如果一个星号 ( **&#42;** ) 使用时，情况的第一个可用的驱动程序字母。 用户然后可以访问导出的文件系统，就好像它是本地计算机上的驱动器。 当使用不带选项或多个**装载**显示所有已装载 NFS 文件系统有关的信息。

**装载**实用程序是安装 nfs 客户端时才可用。

可以通过使用以下选项和参数**装载**实用程序。


|          术语          |                                                                                                                                                                                                                                                定义                                                                                                                                                                                                                                                |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -o rsize=\<buffersize> |                                                                                                                                                                                            设置的大小以千字节为单位的读取缓冲区。 可接受的值为 1、 2、 4、 8、 16 和 32;默认值为 32 KB。                                                                                                                                                                                            |
| -o wsize=\<buffersize> |                                                                                                                                                                                           设置在写入缓冲区的千字节为单位的大小。 可接受的值为 1、 2、 4、 8、 16 和 32;默认值为 32 KB。                                                                                                                                                                                            |
| -o timeout=\<seconds>  |                                                                                                                                                                       以秒为单位的远程过程调用 (RPC) 设置的超时值。 可接受的值为 0.8、 0.9 以及 1-60; 的范围内的任何整数默认值为 0.8。                                                                                                                                                                       |
|   -o retry=\<number>   |                                                                                                                                                                                             设置为软装载的重试次数。 可接受的值为 1-10; 范围内的整数默认值为 1。                                                                                                                                                                                             |
|     -o mtype={soft     |                                                                                                                                                                                                                                                  硬}                                                                                                                                                                                                                                                   |
|        -o anon         |                                                                                                                                                                                                                                       以匿名用户身份装载。                                                                                                                                                                                                                                       |
|       -o nolock        |                                                                                                                                                                                                                                禁用锁定 (默认值是**启用**)。                                                                                                                                                                                                                                |
|    -o casesensitive    |                                                                                                                                                                                                                         强制区分大小写的服务器上的文件查找。                                                                                                                                                                                                                          |
| -o fileaccess=\<mode>  | 指定在 NFS 共享上创建的新文件的默认权限模式。 指定*模式下*为窗体中的三位数字*ogw*，其中*o*， *g*，并*w*每个数字它表示的访问授予文件的所有者、 组和世界里，分别。 后面的数字必须在范围 0-7 具有以下含义：</br>-   0:不能访问</br>-1: x （执行访问权限）</br>-2: w （写入访问权限）</br>-3: wx</br>-4: r （读取访问）</br>-   5: rx</br>-6: rw</br>-7: rwx |
|    -o lang={euc-jp     |                                                                                                                                                                                                                                                  euc-tw                                                                                                                                                                                                                                                  |
|     -u:\<用户名 >     |                                                                                                                                                                             指定要使用装载共享的用户名称。 如果*用户名*前面没有反斜杠 ( **\\** )，它作为 UNIX 用户名称。                                                                                                                                                                             |
|     -p:\<密码 >     |                                                                                                                                                                                          要使用装载共享的密码。 如果使用星号 ( **&#42;** )，系统将提示输入密码。                                                                                                                                                                                          |

> [!NOTE]