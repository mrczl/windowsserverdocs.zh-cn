---
ms.assetid: 7b22adfa-298d-413c-88d0-1231825b7d4d
title: 动态访问控制方案概述
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f70bd138a16b23f1fbf7bfabc98ee184e3b9ab37
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825568"
---
# <a name="dynamic-access-control-scenario-overview"></a>动态访问控制：方案概述

>适用于：Windows Server 2016 中，Windows Server 2012 R2、 Windows Server 2012

在 Windows Server 2012 中，你可以在文件服务器控制哪些人可以访问信息并审核已访问信息之间应用数据监管。 动态访问控制可用于：  
  
-   通过使用自动和手动文件分类来识别数据。 例如，你可以在整个组织内的文件服务器中标记数据。  
  
-   通过应用采用中央访问策略的网络安全策略来控制对文件的访问。 例如，你可以定义有权访问组织内健康信息的用户。  
  
-   通过对合规性报告和取证分析使用中央审核策略，审核对文件的访问。 例如，你可以确定曾访问高度敏感信息的用户。  
  
-   通过对敏感的 Microsoft Office 文档使用自动 RMS 加密，来应用 Rights Management Services (RMS) 保护。 例如，你可以配置 RMS 对包含“健康保险流通与责任法案 (HIPAA)”信息的所有文档进行加密。  
  
动态访问控制功能基于合作伙伴和行业应用程序可进一步利用的基础结构投资，因而它可以为使用 Active Directory 的组织提供巨大的价值。 该基础结构包括：  
  
-   一种适用于 Windows 的全新授权和审核引擎，它可以处理条件表达式和中央策略。  
  
-   用户声明和设备声明支持的 Kerberos 身份验证。  
  
-   对文件分类基础结构 (FCI) 的改进。  
  
-   RMS 扩展性支持，合作伙伴可以提供加密非 Microsoft 文件的解决方案。  
  
## <a name="in-this-scenario"></a>本方案内容  
以下方案和指南包含在内，作为此内容集的一部分：  
  
## <a name="BKMK_APP"></a>动态访问控制内容指南  
  
|应用场景|评估|规划|部署|操作|  
|------------|------------|--------|----------|-----------|  
|**方案：中心访问策略**<br /><br />创建文件的中央访问策略允许组织集中部署和管理授权策略，包括使用用户声明、设备声明和资源属性的条件表达式。 这些策略建立在合规性与业务监管要求之上。 这些策略在 Active Directory 中创建与托管，因此使得管理和部署更为容易。<br /><br />**跨林部署声明**<br /><br />Windows Server 2012 中 AD DS 保存在每个林中有 '声明词典' 和所有声明中林中使用的类型都在 Active Directory 林级别定义。 有许多方案，其中主体可能要遍历信任边界。 此方案描述了声明如何遍历信任边界。|[动态访问控制：方案概述](Dynamic-Access-Control--Scenario-Overview.md)<br /><br />[跨林部署声明](Deploy-Claims-Across-Forests.md)|[计划：中央访问策略部署](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)<br /><br />-   [若要将业务请求映射到中心访问策略的过程](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_1)<br />-   [动态访问控制管理的委派](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.1)<br />-   [计划中央访问策略的异常机制](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.2)<br /><br />使用用户声明的最佳实践<br /><br />-   [选择正确的配置，以便在用户域中的声明](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DC_OP3)<br />-   [启用用户声明的操作](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.4.2)<br />-   [文件服务器中使用用户声明的考虑事项而无需使用中心访问策略的自定义 Acl](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_5)<br /><br />[使用设备声明和设备安全组](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DeviceClaims)<br /><br />-   [使用静态设备声明的考虑事项](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.1)<br />-   [启用设备声明的操作](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.3)<br /><br />部署工具<br /><br />-   [数据分类工具包](https://go.microsoft.com/fwlink/?LinkId=%20244300)|[部署中心访问策略&#40;演示步骤&#41;](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md)<br /><br />[跨林部署声明&#40;演示步骤&#41;](Deploy-Claims-Across-Forests--Demonstration-Steps-.md)|-建模中心访问策略|  
|**方案：文件访问审核**<br /><br />安全审核是用来帮助维护企业安全的功能最强大的工具之一。 安全审核的主要目标之一就是监管合规。 例如，像 Sarbanes Oxley、HIPAA 和 Payment Card Industry (PCI) 这类的行业标准要求企业遵守与数据安全和隐私权有关的一套严格的规则。 安全审核可以帮助确定此类策略是否存在；由此它们证明是否与这些标准相符。 此外，通过创建可用于取证分析的用户活动记录，安全审核可帮助发现异常的行为、识别并缓和在安全策略方面的差距并阻止不负责任的行为。|[方案：文件访问审核](Scenario--File-Access-Auditing.md)|[规划文件访问审核](Plan-for-File-Access-Auditing.md)|[部署安全审核使用中心审核策略&#40;演示步骤&#41;](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md)|-   [监视应用于文件服务器的中央访问策略](https://technet.microsoft.com/library/jj574188.aspx)<br />-   [监视文件和文件夹相关联的中心访问策略](https://technet.microsoft.com/library/jj574198.aspx)<br />-   [监视文件和文件夹上的资源属性](https://technet.microsoft.com/library/jj574208.aspx)<br />-   [监控声明类型](https://technet.microsoft.com/library/jj574086.aspx)<br />-   [在登录过程中监视用户和设备声明](https://technet.microsoft.com/library/jj574082.aspx)<br />-   [监控中央访问策略和规则定义](https://technet.microsoft.com/library/jj574115.aspx)<br />-   [监控资源属性定义](https://technet.microsoft.com/library/jj574155.aspx)<br />-   [监视可移动存储设备的使用](https://technet.microsoft.com/library/jj574128.aspx)。|  
|**方案：拒绝访问协助**<br /><br />现在，当用户尝试访问文件服务器上的远程文件时，能得到的仅有指示是访问被拒绝。 这将生成支持人员或 IT 管理员请求，它们需要弄清问题是什么，而管理员通常很难从用户那里得到合适的上下文，这使得解决问题更困难了。 <br />在 Windows Server 2012 中，目标是尝试与帮助信息工作者和业务数据所有者处理访问被拒绝问题之前 IT 获取涉及以及何时 IT 涉入，提供快速解决所有正确的信息。 达到这个目标的挑战之一是存在是无法集中处理访问被拒绝和每个应用程序以不同方式处理该用，因此 Windows Server 2012 中的目标之一是改进 Windows 资源管理器的访问受拒体验。|[方案：拒绝访问协助](Scenario--Access-Denied-Assistance.md)|[拒绝访问协助的规划](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)<br /><br />-   [确定拒绝访问协助模式](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.1)<br />-   [确定谁应该处理访问请求](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_12)<br />-   [自定义拒绝访问协助消息](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_13)<br />-   [例外计划](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.4)<br />-   [确定如何拒绝访问协助部署](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.5)|[部署拒绝访问协助&#40;演示步骤&#41;](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md)||  
|**方案：基于分类的 Office 文档加密**<br /><br />敏感信息的保护主要与为组织降低风险有关。 诸如 HIPAA 或支付卡行业数据安全标准 (PCI-DSS) 等各种合规性规章制度，都规定了信息加密，而且出于商业考虑也需要加密敏感的业务信息。 但是，加密信息的成本比较高，这可能会损害企业的生产力。 因此，对于信息加密，组织往往采用不同的方法和优先级。 <br />若要支持这种情况下，Windows Server 2012 提供了自动加密敏感 Windows Office 文件基于分类的功能。 这通过文件管理任务来完成，文件管理任务在文件被识别为文件服务器上的敏感文件后几秒钟，为敏感文档调用 Acitve Directory 权限管理服务器 (AD RMS) 保护。|[方案：基于分类的 Office 文档加密](Scenario--Classification-Based-Encryption-for-Office-Documents.md)|[计划部署基于分类的加密的文档](assetId:///14714ba6-d6a2-45e4-aae5-d3318817e52a)|[部署 Office 文件的加密&#40;演示步骤&#41;](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md)||  
|**方案：深入了解你的数据使用分类**<br /><br />对数据和存储资源的依赖在大多数组织的重要性方面持续增长。 IT 管理员面对着监督更大、更复杂存储基础结构的日渐增长的挑战，而同时又担负着确保所有者总开支维持在合理水平的责任。 管理存储资源不再仅仅是涉及数据的量和可用性，还和公司政策的执行有关，和了解如何消耗存储来启用高效利用与合规减轻风险有关。 文件分类基础结构通过自动化分类流程来让你深入了解数据，以便你可以更有效地管理数据。 下列分类方法可用于文件分类基础结构：手动、编程、自动。 此方案重点介绍自动文件分类方法。|[方案：深入了解你的数据使用分类](Scenario--Get-Insight-into-Your-Data-by-Using-Classification.md)|[自动文件分类规划](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955)|[部署自动文件分类&#40;演示步骤&#41;](Deploy-Automatic-File-Classification--Demonstration-Steps-.md)||  
|**方案：在文件服务器上实现信息的保留期**<br /><br />保留期是文档过期前应保存的时间量。 组织不同，保留期可能也不相同。 可以将文件夹中的文件分类为具有短、中或长保留期，然后为每个保留期分配时间范围。 你可能想要通过将文件合法保留来无限期保留。 <br />文件分类基础结构和文件服务器资源管理器使用文件管理任务和文件分类，将保留期应用到一系列文件上。 可给文件夹分配一个保留期，然后使用文件管理任务配置分配的保留期的持续时间。 当文件夹中的文件将要过期时，文件所有者会收到一封通知邮件。 也可将文件分类为合法保留，这样文件管理任务就不会使文件过期。|[方案：在文件服务器上实现信息的保留期](Scenario--Implement-Retention-of-Information-on-File-Servers.md)|[规划文件服务器上的信息的保留期](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)|[部署文件服务器上实现信息的保留期&#40;演示步骤&#41;](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md)||  
  
> [!NOTE]  
> ReFS（弹性文件系统）不支持动态访问控制。  
  
## <a name="BKMK_LINKS"></a>另请参阅  
  
|内容类型|参考|  
|----------------|--------------|  
|**产品评估**|-   [动态访问控制审阅者指南](https://go.microsoft.com/fwlink/?LinkId=244309)<br />-   [动态访问控制开发人员指南](https://go.microsoft.com/fwlink/?LinkId=245870)|  
|**规划**|-   [计划中央访问策略部署](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)<br />-   [规划文件访问审核](Plan-for-File-Access-Auditing.md)|  
|**部署**|-   [Active Directory 部署](https://go.microsoft.com/fwlink/p/?LinkID=238318)<br />-   [文件和存储服务部署](https://go.microsoft.com/fwlink/?LinkID=24430)|  
|**操作**|[动态访问控制 PowerShell 参考](https://go.microsoft.com/fwlink/?LinkId=243150)|  
|**工具和设置**|[数据分类工具包](https://go.microsoft.com/fwlink/?LinkID=244300)|  
|**社区资源**|[目录服务论坛](https://social.technet.microsoft.com/Forums/winserverDS/threads)|  
  

