---
title: nslookup lserver
description: 'Windows 命令主题 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2f2f787915f2b941d6c098d44de1bb0e04dbd491
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436912"
---
# <a name="nslookup-lserver"></a>nslookup lserver

>适用于：Windows 服务器 （半年频道），Windows Server 2016 中，Windows Server 2012 R2、 Windows Server 2012

默认服务器更改到指定的域名系统 (DNS) 域。
## <a name="syntax"></a>语法
```
lserver <DNSDomain> 
```
## <a name="parameters"></a>Parameters

|    参数    |                      描述                      |
|-----------------|-------------------------------------------------------|
|   <DNSDomain>   | 指定的默认服务器的新 DNS 域。  |
| {help &#124; ?} | 显示的短摘要**nslookup**子命令。 |

## <a name="remarks"></a>备注
- **Lserver**命令使用初始服务器来查找指定的 DNS 域有关的信息。 这是与此相反**server**命令，使用当前的默认服务器。
  ## <a name="additional-references"></a>其他参考
  [命令行语法解答](command-line-syntax-key.md)
  [nslookup 服务器](nslookup-server.md)