---
title: AD FS 故障排除-证书
description: 本文档介绍了典型的证书问题。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 42fdce936bb4a6f25b456c4a96c7b99f650e6033
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860578"
---
# <a name="ad-fs-troubleshooting---certificates"></a>AD FS 故障排除-证书
AD FS 要求以下证书才能正常工作。  如果其中的任何尚未安装或配置不正确可能出现的问题。  

## <a name="required-certificates"></a>所需的证书
AD FS 要求以下证书：



- **联合身份验证信任**– 此要求的声明提供程序和信赖方联合身份验证服务器的受信任的根存储中存在的链接到相互信任的 Internet 根证书颁发机构 (CA) 的证书实现交叉证书设计了每一方具有与其伙伴交换其根 CA 或自签名证书已导入的每一侧在适当的位置。
- **令牌签名**– 每个联合身份验证服务的计算机需要的令牌签名证书。  必须由信赖方联合身份验证服务器信任声明提供程序令牌签名证书。 信赖方令牌签名证书必须受从 RP 联合身份验证服务器接收令牌的所有应用程序。
- **安全套接字层 (SSL)** – 为联合身份验证服务的 SSL 证书必须存在于联合身份验证服务器代理计算机上受信任的存储和受信任的证书颁发机构 (CA) 存储到有一个有效的链。
- **证书吊销列表 (CRL)** – 任何证书具有 CRL 发布，CRL 必须可供所有客户端和服务器需要访问该证书。

如果上述任何未正确配置，AD FS 将无法工作。

## <a name="common-things-to-check-with-certificates"></a>要检查证书的常见事项
下面是可能会出现，且尝试解决证书问题时应验证的操作的列表。

- 请确保该证书是受信任
    - 需要客户端信任的 SSL 证书
    - 需要的信赖方信任令牌签名证书
- 检查信任链的链需要有效的每个证书。
- 验证证书过期日期
- 检查证书吊销列表 (CRL) 可访问性
    - 请确保填充 CDP 字段
    - 手动浏览到 CDP
- 请确保该证书尚未吊销

## <a name="common-certificate-errors"></a>常见证书错误
下表是一系列常见的错误和可能的原因。

|Event|原因|分辨率
|-----|-----|-----|
|事件 249-证书无法找到的证书存储中。 在证书滚动更新方案中，这可能会导致联合身份验证服务是签名或解密使用此证书时失败。|相关的证书不在本地证书存储或服务帐户没有对证书的私钥的权限。|确保证书安装在 AD FS 服务器上的 LocalMAchine\My 存储中。 请确保 AD FS 服务帐户具有读取访问权限的证书的私钥。|
|事件 315-在尝试生成签名证书声明提供方信任的证书链的过程时出错。|证书已吊销。</br></br>无法验证证书链。</br></br>证书已过期或尚未生效。|请确保证书有效，并且未被吊销。</br></br>确保 CRL 可访问。|
|事件 316-在尝试生成签名证书的信赖方信任的证书链的过程时出错。|证书已吊销。</br></br>无法验证证书链。</br></br>证书已过期或尚未生效。|请确保证书有效，并且未被吊销。</br></br>确保 CRL 可访问。|
|事件 317-在尝试生成信赖方信任加密证书的证书链的过程时出错。|证书已吊销。</br></br>无法验证证书链。</br></br>证书已过期或尚未生效。|请确保证书有效，并且未被吊销。</br></br>确保 CRL 可访问。|
|事件 319-出错时正在生成的客户端证书的证书链。|证书已吊销。</br></br>无法验证证书链。</br></br>证书已过期或尚未生效。|请确保证书有效，并且未被吊销。</br></br>确保 CRL 可访问。|
|事件 360-已请求到证书传输终结点，但请求中未包括客户端证书。|不受信任的根 CA 颁发的客户端证书。</br></br>客户端证书已过期。</br></br>客户端证书自签名证书和不受信任。|请确保根 CA 颁发的客户端证书是受信任的根存储区中存在。</br></br>请确保客户端证书未过期。</br></br>如果客户端证书是自签名证书，请确保验证它已添加到受信任证书的列表或自签名的证书替换为受信任的证书。|
|事件 374-为声明提供方信任的加密证书构建证书链时出错。|证书已吊销。</br></br>无法验证证书链。</br></br>证书已过期或尚未生效。|请确保证书有效，并且未被吊销。</br></br>确保 CRL 可访问。|
|事件 381-在尝试生成配置证书的证书链的过程时出错。|一个配置为使用 AD FS 服务器上的证书已过期或已被吊销。|确保所有已配置的证书尚未吊销，并且尚未过期。|
|事件 385-检测到 AD FS，需要手动更新 AD FS 配置数据库中的一个或多个证书。|一个配置为使用 AD FS 服务器上的证书已过期或即将达到其到期日期。|更新已过期或即将-到-过期的证书进行更换。 （如果您正在使用自签名的证书和启用自动证书滚动更新，忽略此错误可能是因为它将自行解决。）|
|事件 387-检测到 AD FS，一个或多个联合身份验证服务中指定的证书未由 AD FS Windows 服务的服务帐户可以访问。|AD FS 服务帐户没有读取的权限的一个或多个已配置证书的私钥。|确保 AD FS 服务帐户具有读取权限的所有已配置证书的私钥。|
|事件 389-检测到 AD FS，一个或多个你信任的要求其进行手动更新，因为它们已过期或即将过期的证书。|一个配置的合作伙伴的证书已过期或即将过期。 这可以将应用到声明提供方信任或信赖方信任。|如果你手动创建此信任，请手动更新证书配置。 如果联合身份验证元数据用于创建信任关系，只要合作伙伴更新证书的证书将自动更新。|




## <a name="next-steps"></a>后续步骤

- [AD FS 进行故障排除](ad-fs-tshoot-overview.md)
 