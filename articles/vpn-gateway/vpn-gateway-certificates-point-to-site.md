---
title: "ポイント対サイトの証明書の作成とエクスポート: PowerShell: Azure | Microsoft Docs"
description: "この記事では、自己署名ルート証明書の作成、公開キーのエクスポート、クライアント証明書の生成を Windows 10 で PowerShell を使用して行う手順について説明します。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: cherylmc
ms.translationtype: Human Translation
ms.sourcegitcommit: 5e92b1b234e4ceea5e0dd5d09ab3203c4a86f633
ms.openlocfilehash: 1bfcb8683669770d6dd927cbde53a683bbc1d56e
ms.contentlocale: ja-jp
ms.lasthandoff: 05/10/2017


---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell"></a>PowerShell を使用したポイント対サイト接続の証明書の生成とエクスポート

この記事では、自己署名ルート証明書の作成方法とクライアント証明書の生成方法について説明します。 この記事には、ポイント対サイト構成の手順や、ポイント対サイトについてよく寄せられる質問は含まれません。 これらの情報について、次のリストから「ポイント対サイトの構成」のいずれかの記事を選択してご覧ください。

> [!div class="op_single_selector"]
> * [自己署名証明書の作成 - PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [自己署名証明書の作成 - Makecert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [ポイント対サイトの構成 - リソース マネージャー - Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [ポイント対サイトの構成 - リソース マネージャー - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [ポイント対サイトの構成 - クラシック - Azure Portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

ポイント対サイト接続では、認証に証明書を使用します。 ポイント対サイト接続を構成するときに、ルート証明書の公開キー (.cer ファイル) を Azure にアップロードする必要があります。 さらに、クライアント証明書は、ルート証明書から生成され、VNet に接続する各クライアント コンピューターにインストールされる必要があります。 クライアント証明書を使用してクライアントを認証できます。


> [!NOTE]
> この記事の手順は、Windows 10 を実行するコンピューターで実行する必要があります。 証明書の生成に必要な PowerShell コマンドレットは、Windows 10 オペレーティング システムの一部であり、その他のバージョンの Windows では機能しません。 これらのコマンドレットは、証明書の生成にのみ使用します。 証明書は、生成されると、サポートされるクライアントのあらゆるオペレーティング システムにインストールできます。 Windows 10 のコンピューターを使用できない場合は、makecert を使用して証明書を生成できます。 ただし、makecert を使用して生成した証明書は、ポイント対サイトとの互換性はありますが、SHA-2 ではありません。 makecert の手順については、「[Create certificates using makecert (makecert を使用した証明書の作成)](vpn-gateway-certificates-point-to-site-makecert.md)」をご覧ください。 PowerShell または makecert のいずれかを使用して作成した証明書は、証明書の作成に使用したオペレーティング システムだけでなく、[サポートされるクライアントのあらゆるオペレーティング システム](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq)にインストールできます。
> 
>

## <a name="rootcert"></a>自己署名ルート証明書の作成

次の手順では、Windows 10 で PowerShell を使用して自己署名ルート証明書を作成する方法を説明します。 これらの手順で使用されているコマンドレットとパラメーターは、Windows 10 オペレーティング システムの一部であり、PowerShell バージョンの一部ではありません。 作成した証明書を Windows 10 にしかインストールできないという意味ではありません。 作成した証明書は、サポートされているあらゆるクライアントにインストールできます。 サポートされるクライアントの詳細については、「[ポイント対サイト接続に関してよく寄せられる質問](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq)」を参照してください。

1. Windows 10 を実行しているコンピューターから、昇格された特権を使用して Windows PowerShell コンソールを開きます。
2. 次の例を使用して、自己署名ルート証明書を作成します。 次の例では、"P2SRootCert" という名前の自己署名ルート証明書が作成され、"Certificates-Current User\Personal\Certificates" に自動的にインストールされます。 *certmgr.msc*、または*ユーザー証明書の管理*を開くと、証明書を表示できます。

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>公開キー (.cer) のエクスポート

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

エクスポートした .cer ファイルは Azure にアップロードする必要があります。 手順については、[ポイント対サイト接続の構成](vpn-gateway-howto-point-to-site-rm-ps.md#upload)に関するページをご覧ください。

### <a name="export-the-self-signed-root-certificate-and-public-key-to-store-it-optional"></a>自己署名ルート証明書と証明書を保存するための公開キーのエクスポート (省略可能)

自己署名ルート証明書をエクスポートし、安全に保管することもできます。 必要に応じて、後から別のコンピューターにインストールして、さらに多くのクライアント証明書を生成したり、別の .cer ファイルをエクスポートしたりできます。 自己署名ルート証明書を .pfx としてエクスポートするには、ルート証明書を選択し、「[クライアント証明書をエクスポートする](#clientexport)」と同じ手順を実行します。

## <a name="clientcert"></a>クライアント証明書の生成

ポイント対サイトで VNet に接続するすべてのクライアント コンピューターには、クライアント証明書がインストールされている必要があります。 自己署名ルート証明書からクライアント証明書を生成し、そのクライアント証明書をエクスポートしてインストールします。 クライアント証明書がインストールされていない場合は、認証が失敗します。 

次の手順では、自己署名ルート証明書からクライアント証明書を生成する方法を示しています。 同じルート証明書から複数のクライアント証明書を生成できます。 以下の手順を使用してクライアント証明書を生成すると、証明書の生成に使用したコンピューターにクライアント証明書が自動的にインストールされます。 クライアント証明書を別のクライアント コンピューターにインストールする場合は、その証明書をエクスポートできます。

Windows 10 では、次の PowerShell の手順を使用してクライアント証明書を生成する必要があります。 これらの手順で使用されているコマンドレットとパラメーターは、Windows 10 オペレーティング システムの一部であり、PowerShell バージョンの一部ではありません。 作成した証明書を Windows 10 にしかインストールできないという意味ではありません。 サポートされるクライアントの詳細については、「[ポイント対サイト接続に関してよく寄せられる質問](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq)」を参照してください。

### <a name="example-1"></a>例 1

この例では、前のセクションで宣言した '$cert' 変数を使用します。 自己署名ルート証明書の作成後に PowerShell コンソールを閉じた場合または新しい PowerShell コンソール セッションで追加のクライアント証明書を作成している場合は、[例 2](#ex2) の手順を使用してください。

クライアント証明書を生成するには、例を変更して実行します。 次の例を変更せずに実行した場合、クライアント証明書の名前は "P2SChildCert" になります。  子証明書に別の名前を付ける場合は、CN 値を変更します。 この例を実行する際に TextExtension を変更しないでください。 生成したクライアント証明書は、コンピューターの "Certificates - Current User\Personal\Certificates" に自動的にインストールされます。

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>例 2

追加のクライアント証明書を作成している場合、または自己署名ルート証明書の作成に使用したのと同じ PowerShell セッションを使用していない場合は、次の手順を使用してください。

1. コンピューターにインストールされている自己署名ルート証明書を特定します。 次のコマンドレットは、コンピューターにインストールされている証明書の一覧を返します。

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. 返された一覧でサブジェクト名を探し、その横にある拇印をテキスト ファイルにコピーします。 次の例では、2 つの証明書があります。 CN 名は、子証明書の生成元となる自己署名ルート証明書の名前です。 この場合は "P2SRootCert" です。

        Thumbprint                                Subject

        AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
        7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert


3. 前の手順の拇印を使用して、ルート証明書の変数を宣言します。 THUMBPRINT を、子証明書の生成元となるルート証明書の拇印に置き換えます。

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  たとえば、前の手順の P2SRootCert の拇印を使用すると、変数は次のようになります。

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```    

4.  クライアント証明書を生成するには、例を変更して実行します。 次の例を変更せずに実行した場合、クライアント証明書の名前は "P2SChildCert" になります。 子証明書に別の名前を付ける場合は、CN 値を変更します。 この例を実行する際に TextExtension を変更しないでください。 生成したクライアント証明書は、コンピューターの "Certificates - Current User\Personal\Certificates" に自動的にインストールされます。

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="clientexport"></a>クライアント証明書のエクスポート   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]
    

## <a name="install"></a>エクスポートしたクライアント証明書のインストール

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>次のステップ

引き続きポイント対サイト構成を使用します。 

* **Resource Manager** デプロイメント モデルの手順については、[VNet へのポイント対サイト接続の構成](vpn-gateway-howto-point-to-site-resource-manager-portal.md)に関する記事を参照してください。 
* **クラシック** デプロイメント モデルの手順については、[VNet へのポイント対サイト VPN 接続の構成 (クラシック)](vpn-gateway-howto-point-to-site-classic-azure-portal.md) に関する記事を参照してください。
