---
title: 初始化 HGS 群集在堡垒林中使用 TPM 模式
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: ac6407f9f23780dc62ff7d99fe0daf0f81f79f72
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832138"
---
# <a name="initialize-the-hgs-cluster-using-tpm-mode-in-an-existing-bastion-forest"></a>初始化 HGS 群集在现有的堡垒林中使用 TPM 模式

>适用于：Windows Server 2019，Windows Server （半年频道），Windows Server 2016

Active Directory 域服务将在计算机上安装，但应保留未配置。

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

在继续之前，确保你已为主机保护者服务预备群集对象并授予已登录用户**完全控制**Active Directory 中 VCO 和 CNO 对象。
虚拟计算机对象名称需要传递给`-HgsServiceName`参数与群集名称`-ClusterName`参数。

> [!TIP]
> 仔细检查你的 AD 域控制器，以确保您的群集对象已被复制到所有域控制器然后再继续。

如果要使用基于 PFX 的证书，HGS 服务器上运行以下命令：

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustTpm
```

如果使用 （如、 由 HSM 支持的证书和非可导出的证书） 在本地计算机上安装的证书，使用`-SigningCertificateThumbprint`和`-EncryptionCertificateThumbprint`参数相反。

## <a name="next-step"></a>下一步

>[!div class="nextstepaction"]
[安装 TPM 根证书](guarded-fabric-install-trusted-tpm-root-certificates.md)