---
ms.assetid: 663a2482-33d1-4c19-8607-2e24eef89fcb
title: 使用 WID 的联合服务器场
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f0f3d8c70a41d512e7cd33282524bc401ce84600
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191428"
---
# <a name="federation-server-farm-using-wid"></a>使用 WID 的联合服务器场

Active Directory 联合身份验证服务的默认拓扑\(AD FS\)是使用 Windows 内部数据库的联合身份验证服务器场\(WID\)，最多五个托管的联合身份验证服务器，它包含在组织的联合身份验证服务。 在此拓扑中，AD FS 使用 WID 作为存储的所有联合服务器加入到该场的 AD FS 配置数据库。 该场针对场中的每台服务器，在此配置数据库中复制和维护联合身份验证服务数据。  
  
在场中创建第一台联合服务器的操作也将创建一项新的联合身份验证服务。 当你使用 WID 的 AD FS 配置数据库时，在该场中创建第一个联合服务器称为*主联合服务器*。 这意味着此计算机配置与读取\/编写的 AD FS 配置数据库副本。  
  
为此服务器场配置的所有其他联合服务器称为*辅助联合服务器*因为它们必须将复制到只读主联合服务器所做的任何更改\-仅它们在本地存储的 AD FS 配置数据库的副本。  
  
> [!NOTE]  
> 我们建议在负载中的至少两台联合服务器使用\-均衡的配置。  
  
## <a name="deployment-considerations"></a>部署注意事项  
本部分介绍有关目标的受众、 权益和限制，与此部署拓扑相关联的各种注意事项。  
  
### <a name="who-should-use-this-topology"></a>应使用此拓扑的用户？  
  
-   具有 100 个或更少需要提供其内部用户的配置的信任关系的组织\(登录到以物理方式连接到公司网络的计算机\)用于单一登录\-上\(SSO\)访问联合应用程序或服务  
  
-   想要为其内部的用户提供 SSO 访问 Microsoft Online Services 或 Microsoft Office 365 的组织  
  
-   较小的组织需要冗余、 可缩放服务  
  
> [!NOTE]  
> 更大的数据库的组织应考虑使用[联合服务器场使用 SQL Server](Federation-Server-Farm-Using-SQL-Server.md)部署拓扑，稍后在本部分中介绍。 从网络外部日志的用户的组织应考虑使用[联合服务器场使用 WID 和代理](Federation-Server-Farm-Using-WID-and-Proxies.md)拓扑或[联合服务器场使用 SQL Server](Federation-Server-Farm-Using-SQL-Server.md)拓扑。  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>使用此拓扑的好处是什么？  
  
-   提供对内部用户的 SSO 访问  
  
-   数据和联合身份验证服务冗余纳入\(每台联合服务器将更改复制到同一场中的其他联合身份验证服务器\)  
  
-   服务器场可通过添加最多五个联合身份验证服务器来横向扩展  
  
-   WID 随 Windows;因此，无需购买 SQL Server  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>使用此拓扑的限制是什么？  
  
-   WID 场的限制为五个联合身份验证服务器。 有关详细信息，请参阅 [AD FS 部署拓扑注意事项](AD-FS-Deployment-Topology-Considerations.md)。  
  
-   WID 场不支持令牌重放检测或项目分辨率\(安全断言标记语言的一部分\(SAML\)协议\)。  
  
## <a name="server-placement-and-network-layout-recommendations"></a>服务器位置和网络布局建议  
当准备好开始部署您的网络中的此拓扑，您应计划网络负载平衡之后在公司网络中放置的所有联合身份验证服务器\(NLB\)可以配置为 NLB 群集的主机使用一个专用群集域名系统\(DNS\)名称和群集 IP 地址。  
  
> [!NOTE]  
> 此群集 DNS 名称必须与联合身份验证服务名称，例如，fs.fabrikam.com 匹配。  
  
NLB 主机可以使用此 NLB 群集，以便分配对单个联合身份验证服务器的客户端请求中定义的设置。 下图显示了如何虚构 Fabrikam，Inc.，公司设置了其使用两个部署的第一阶段\-计算机的联合服务器场\(fs1 和 fs2\)以及 WID 和 DNS 服务器的位置和有线公司网络到一台 NLB 主机。  
  
![使用 WID 服务器场](media/FarmWID.gif)  
  
> [!NOTE]  
> 如果在此单个 NLB 主机故障，用户不能访问联合应用程序或服务。 如果你的业务要求不允许存在单点故障，则应添加其他 NLB 主机。  
  
有关如何使用联合身份验证服务器配置为使用你的网络环境的详细信息，请参阅[联合身份验证服务器的名称解析要求](Name-Resolution-Requirements-for-Federation-Servers.md)AD FS 设计指南中。  
  
## <a name="see-also"></a>请参阅
[Windows Server 2012 中的 AD FS 设计指南](AD-FS-Design-Guide-in-Windows-Server-2012.md)