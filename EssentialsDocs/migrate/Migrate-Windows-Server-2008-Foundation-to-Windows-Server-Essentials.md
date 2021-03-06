---
title: 将 Windows Server 2008 Foundation 迁移到 Windows Server Essentials
description: 介绍如何使用 Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f22fc0a4-cb82-4e60-afe6-2d03145745e7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 22721833d3ba97c7860c949764d565415bbc7cab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813758"
---
# <a name="migrate-windows-server-2008-foundation-to-windows-server-essentials"></a>将 Windows Server 2008 Foundation 迁移到 Windows Server Essentials

>适用于：Windows Server 2016 Essentials，Windows Server 2012 R2 Essentials 中，Windows Server 2012 Essentials

本指南介绍了如何将现有 Windows Server 2008 Foundation 域迁移到新硬件上的 Windows Server® 2012 Essentials 以及之后如何迁移设置和数据。 本指南还描述如何完成迁移后从 Windows Server Essentials 网络中删除现有的服务器。  
  
> [!NOTE]
>  若要避免在迁移期间出现问题，Windows Server Essentials 产品开发团队强烈建议在开始迁移之前阅读此文档。  
  
## <a name="additional-resources"></a>其他资源  
 有关可帮助指导你完成迁移过程的其他信息、工具和社区资源的链接，请访问 [Windows Small Business Server 迁移](https://go.microsoft.com/fwlink/?LinkId=217520)。  
  
## <a name="terms-and-definitions"></a>术语和定义  
 **源服务器：** 作为迁移设置和数据的来源的现有服务器。  
  
 **目标服务器：** 作为迁移设置和数据的目标的新服务器。  
  
## <a name="migration-process-summary"></a>迁移过程摘要  
 此迁移指南包括下列步骤：  
  

1.  [源服务器以进行 Windows Server Essentials 迁移准备](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)。  必须确保源服务器和网络已准备好执行迁移操作。 本节指导你完成下列操作：备份源服务器，评估源服务器系统的运行状况，安装最新的 Service Pack 和修补程序，以及验证网络配置。  
  
2.  [在迁移模式下安装 Windows Server Essentials](Install-Windows-Server-Essentials-in-migration-mode.md)。  本部分介绍在迁移模式下在目标服务器上安装 Windows Server Essentials 时应采取的步骤。  
  
3.  [将计算机加入到新的 Windows Server Essentials 网络](Join-computers-to-the-new-Windows-Server-Essentials-network.md)。  本部分介绍客户端计算机加入新的 Windows Server Essentials 网络以及更新组策略设置。  
  
4.  [将 Windows Server 2008 Foundation 设置和数据移到目标服务器](Move-Windows-Server-2008-Foundation-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)。  本节提供从源服务器迁移数据和设置的相关信息。  
  
5.  [降级和删除源服务器从新的 Windows Server Essentials 网络](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)。  从网络中删除源服务器之前，必须强制执行组策略更新并将源服务器降级。  
  
6.  [为 Windows Server Essentials 迁移执行迁移后任务](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md)。  在完成所有设置和数据都迁移到 Windows Server Essentials 后，您可能希望将获得允许的计算机映射到用户帐户。  
  
7.  [运行 Windows Server Essentials 最佳做法分析器](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)。  在完成设置和迁移到 Windows Server Essentials 的数据后，应运行 Windows Server Essentials BPA。  

1.  [源服务器以进行 Windows Server Essentials 迁移准备](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)。  必须确保源服务器和网络已准备好执行迁移操作。 本节指导你完成下列操作：备份源服务器，评估源服务器系统的运行状况，安装最新的 Service Pack 和修补程序，以及验证网络配置。  
  
2.  [在迁移模式下安装 Windows Server Essentials](../migrate/Install-Windows-Server-Essentials-in-migration-mode.md)。  本部分介绍在迁移模式下在目标服务器上安装 Windows Server Essentials 时应采取的步骤。  
  
3.  [将计算机加入到新的 Windows Server Essentials 网络](../migrate/Join-computers-to-the-new-Windows-Server-Essentials-network.md)。  本部分介绍客户端计算机加入新的 Windows Server Essentials 网络以及更新组策略设置。  
  
4.  [将 Windows Server 2008 Foundation 设置和数据移到目标服务器](../migrate/Move-Windows-Server-2008-Foundation-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)。  本节提供从源服务器迁移数据和设置的相关信息。  
  
5.  [降级和删除源服务器从新的 Windows Server Essentials 网络](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)。  从网络中删除源服务器之前，必须强制执行组策略更新并将源服务器降级。  
  
6.  [为 Windows Server Essentials 迁移执行迁移后任务](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md)。  在完成所有设置和数据都迁移到 Windows Server Essentials 后，您可能希望将获得允许的计算机映射到用户帐户。  
  
7.  [运行 Windows Server Essentials 最佳做法分析器](../migrate/Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)。  在完成设置和迁移到 Windows Server Essentials 的数据后，应运行 Windows Server Essentials BPA。  

  
 某些迁移过程需要以管理员身份打开命令提示符窗口。  
  
###  <a name="BKMK_OpenACommandPromptAsAdmin"></a> 若要以管理员身份打开命令提示符窗口，在源服务器上  
  
1.  单击“开始” 。  
  
2.  在搜索框中，键入“cmd”。  
  
3.  在结果列表中，右键单击“cmd”，然后单击“以管理员身份运行”。  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>在目标服务器上以管理员身份打开命令提示符窗口的步骤  
  
1.  在“开始”屏幕的搜索框中，键入 **cmd**。  
  
2.  在结果列表中，右键单击“cmd”，然后单击“以管理员身份运行”。
