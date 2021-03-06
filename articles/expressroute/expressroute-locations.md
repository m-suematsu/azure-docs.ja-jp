---
title: "接続プロバイダーと場所: Azure ExpressRoute | Microsoft Docs"
description: "この記事では、サービスが提供されている場所と Azure リージョンに接続する方法の詳細について説明します。 接続プロバイダーごとにソートされています。"
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: c878513a-d594-42ad-8b0e-403efd0c4b25
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kaanan
ms.translationtype: Human Translation
ms.sourcegitcommit: c785ad8dbfa427d69501f5f142ef40a2d3530f9e
ms.openlocfilehash: 72f310a489ca458719600d2fba5b9ca630d44e2f
ms.contentlocale: ja-jp
ms.lasthandoff: 05/26/2017


---
# <a name="expressroute-partners-and-peering-locations"></a>ExpressRoute パートナーとピアリングの場所

> [!div class="op_single_selector"]
> * [プロバイダー別の場所](expressroute-locations.md)
> * [場所別のプロバイダー](expressroute-locations-providers.md)


この記事の表では、ExpressRoute 接続プロバイダー、ExpressRoute の地理的範囲、ExpressRoute でサポートされる Microsoft クラウド サービス、ExpressRoute システム インテグレーター (SI) に関する情報を提供します。

## <a name="partners"></a>ExpressRoute 接続プロバイダー
ExpressRoute は、すべての Azure のリージョンと場所でサポートされています。 次のマップは Azure のリージョンと ExpressRoute の場所を一覧しています。 ExpressRoute の場所は、Microsoft がいくつかのサービス プロバイダーと接続している場所を示します。

![場所のマップ][0]

地理的リージョン内の少なくとも 1 つの ExpressRoute の場所に接続している場合は、その地理的リージョン内のすべてのリージョンの Azure サービスにアクセスできます。

### <a name="azure-regions-to-expressroute-locations-within-a-geopolitical-region"></a>地理的リージョン内の Azure リージョンと ExpressRoute の場所の対応
次の表は、地理的リージョン、ExpressRoute の場所、Azure リージョンをまとめたものです。

| **地理的リージョン** | **Azure リージョン** | **ExpressRoute の場所** |
| --- | --- | --- |
| **北米** |米国東部、米国西部、米国東部 2、米国西部 2、米国中部、米国中南部、米国中北部、米国中西部、カナダ中部、カナダ東部 |アトランタ、シカゴ、ダラス、デンバー、ラスベガス、ロサンゼルス、マイアミ、ニューヨーク、シアトル、シリコン バレー、ワシントン DC、モントリオール、ケベックシティ、トロント |
| **南アメリカ** |ブラジル南部 |サンパウロ |
| **ヨーロッパ** |北ヨーロッパ、西ヨーロッパ、英国西部、英国南部 |アムステルダム、ダブリン、ロンドン、ニューポート (ウェールズ)、パリ |
| **アジア** |東アジア、東南アジア |香港、シンガポール |
| **日本** |西日本、東日本 |大阪、東京 |
| **オーストラリア** |オーストラリア東部、オーストラリア南東部 |メルボルン、シドニー |
| **インド** |インド西部、インド中部、インド南部 |チェンナイ、ムンバイ |
| **韓国** |韓国中部、韓国南部 |釜山、ソウル |

### <a name="regions-and-geopolitical-boundaries-for-national-clouds"></a>各国のクラウドのリージョンと地理的境界
次の表は、国内のクラウドのリージョンと地政学的境界に関する情報をまとめたものです。

| **地理的リージョン** | **Azure リージョン** | **ExpressRoute の場所** |
| --- | --- | --- |
| **米国政府のクラウド** |米国政府アイオワ、米国政府バージニア、US DoD 中部、US DoD 東部  |シカゴ、ダラス、ニューヨーク、シアトル、シリコン バレー、ワシントン DC |
| **中国** |中国北部、中国東部 |北京、上海 |
| **ドイツ** |ドイツ中部、ドイツ東部 |ベルリン、フランクフルト |

標準の ExpressRoute SKU では、地理的リージョン間の接続はサポートされていません。 グローバル接続に対応するには、ExpressRoute Premium アドオンを有効にする必要があります。 国内のクラウド環境には接続できません。 国内のクラウド環境に接続する必要がある場合、接続プロバイダーにご相談ください。

## <a name="locations"></a>接続プロバイダーの場所

次の表に、サービス プロバイダー別の場所を示します。 場所別の使用可能なプロバイダーを確認する場合は、[場所別のサービス プロバイダー](expressroute-locations-providers.md#locations)に関するページを参照してください。


### <a name="production-azure"></a>運用 Azure
| **サービス プロバイダー** | **Microsoft Azure** | **Office 365 および Dynamics 365** | **場所** |
| --- | --- | --- | --- |
| **[AARNet](https://www.aarnet.edu.au/network-and-services/cloud-services-applications/azure-expressroute/)** |サポートされています |サポートされています |メルボルン、シドニー |
| **Airtel** | 近日対応予定 | 近日対応予定 | チェンナイ、ムンバイ |
| **[Aryaka Networks](http://www.aryaka.com/)** |サポートされています |サポートされています |アムステルダム、ダラス、香港、シリコン バレー、シンガポール、東京、ワシントン DC |
| **[AT&T NetBond](https://www.synaptic.att.com/clouduser/html/productdetail/ATT_NetBond.htm)** |サポートされています |サポートされています |アムステルダム、シカゴ、ダラス、ロンドン、シリコン バレー、シンガポール、シドニー、ワシントン DC |
| **[Bell Canada](https://business.bell.ca/shop/enterprise/cloud-connect-access-to-cloud-partner-services)** |サポートされています |サポートされています |モントリオール、トロント |
| **[British Telecom](http://www.globalservices.bt.com/uk/en/news/bt_to_provide_connectivity_to_microsoft_azure)** |サポートされています |サポートされています |アムステルダム、香港、ロンドン、シリコン バレー、シンガポール、シドニー、東京、ワシントン DC |
| **[CenturyLink](http://www.centurylink.com/business/enterprise/services/data-network/mpls-vpn.html)** |近日対応予定 |近日対応予定 |シリコン バレー |
| **China Telecom Global** |サポートされています |サポートされていません |香港特別行政区 |
| **[Cologix](http://www.cologix.com/solutions/cloud-connect/public-clouds/microsoft-cloud/)** |サポートされています |サポートされています |ダラス、モントリオール、トロント |
| **[Colt](http://www.colt.net/uk/en/news/colt-announces-dedicated-cloud-access-for-microsoft-azure-services-en.htm)** |サポートされています |サポートされています |アムステルダム、ダブリン、ロンドン、東京 |
| **Comcast** |サポートされています |サポートされています |シカゴ、シリコン バレー、ワシントン DC |
| **Console**| サポートされています | サポートされています |シリコン バレー、トロント |
| **[CoreSite](http://www.coresite.com/solutions/cloud-services/public-cloud-providers/microsoft-azure-expressroute)** |サポートされています |サポートされています |デンバー、ロサンゼルス、ニューヨーク |
| **[Equinix](http://www.equinix.com/partners/microsoft-azure/)** |サポートされています |サポートされています |アムステルダム、アトランタ、シカゴ、ダラス、香港、ロンドン、ロサンゼルス、メルボルン、ニューヨーク、大阪、パリ、サンパウロ、シアトル、シリコン バレー、シンガポール、シドニー、東京、トロント、ワシントン DC |
| **euNetworks** |サポートされています |サポートされています |アムステルダム |
| **GÉANT** |サポートされています |サポートされています |アムステルダム |
| **[Global Cloud Xchange (GCX)] (http://globalcloudxchange.com/cloud-platform/cloud-x-fusion/cloud-x-fusion-for-azure/)** | サポートされています| サポートされています | チェンナイ |
| **[InterCloud](https://www.intercloud.com/)** |サポートされています |サポートされています |アムステルダム、ロンドン、シンガポール、ワシントン DC |
| **[Internet Initiative Japan Inc. - IIJ](http://www.iij.ad.jp/en/news/pressrelease/2015/1216-2.html)** |サポートされています |サポートされています |大阪、東京 |
| **Internet Solutions - Cloud Connect** |サポートされています |サポートされています |アムステルダム、ロンドン |
| **[Interxion](http://www.interxion.com/why-interxion/colocate-with-the-clouds/Microsoft-Azure/)** |サポートされています |サポートされています |アムステルダム、ロンドン、パリ |
| **Jisc** |サポートされています |サポートされています |ロンドン |
| **KINX** |サポートされています |サポートされています |ソウル |
| **[KPN](http://www.kpn.com/cloudconnect)** | サポートされています | サポートされています | アムステルダム | 
| **[Level 3 Communications](http://your.level3.com/LP=882?WT.tsrc=02192014LP882AzureVanityAzureText)** |サポートされています |サポートされています |アムステルダム、シカゴ、ダラス、ラスベガス+、ロンドン、シアトル、シリコン バレー、シンガポール、ワシントン DC |
| **LG CNS** |サポートされています |サポートされています |釜山 |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |サポートされています |サポートされています |シカゴ、ダラス、香港、ラスベガス、ロサンゼルス、メルボルン、マイアミ、ニューヨーク、ケベックシティ、シアトル、シリコン バレー、シンガポール、シドニー、トロント、ワシントン DC |
| **MTN** |サポートされています |サポートされています |ロンドン |
| **[Next Generation Data](http://www.nextgenerationdata.co.uk/ngd-cloud-gateway/)** |サポートされています |サポートされています |ニューポート (ウェールズ) |
| **NEXTDC** |サポートされています |サポートされています |メルボルン、シドニー |
| **[NTT Communications](http://www.ntt.com/en/services/network/virtual-private-network.html)** |サポートされています |サポートされています |ロンドン、ロサンゼルス、大阪、シンガポール、東京、ワシントン DC |
| **[Orange](http://www.orange-business.com/en/products/business-vpn-galerie)** |サポートされています |サポートされています |アムステルダム、香港、ロンドン、シリコン バレー、シンガポール、シドニー、ワシントン DC |
| **PCCW Global Limited** |サポートされています |サポートされています |香港特別行政区 |
| **Sejong Telecom** |サポートされています |サポートされています |ソウル |
| **[SIFY](http://telecom.sify.com/azure-expressroute.html)** |サポートされています |サポートされています |チェンナイ |
| **[SingTel](http://info.singtel.com/about-us/news-releases/singtel-provide-secure-private-access-microsoft-azure-public-cloud)** |サポートされています |サポートされています |シンガポール |
| **[Softbank](http://www.softbank.jp/biz/cloud/cloud_access/direct_access_for_az/)** |サポートの有無 |サポートされています |大阪、東京 |
| **[Tata Communications](http://www.tatacommunications.com/lp/izo/azure/azure_index.html)** |サポートされています |サポートされています |アムステルダム、チェンナイ、香港、ロンドン、ムンバイ、シリコン バレー、シンガポール、ワシントン DC |
| **[TeleCity Group](http://www.telecitygroup.com/investor-centre/news_details.htm?locid=03100500400b00d&xml)** |サポートされています |サポートされています |アムステルダム、ダブリン、ロンドン |
| **[Telefonica](https://www.business-solutions.telefonica.com/es/enterprise/solutions/efficient-infrastructure/managed-voice-data-connectivity/)** |サポートされています |サポートされています |アムステルダム+、サンパウロ |
| **[Telehouse - KDDI](http://www.telehouse.net/solutions/cloud-services/cloud-link)** |サポートされています |サポートされています |ロンドン |
| **Telenor** |サポートされています |サポートされています |アムステルダム、ロンドン |
| **[Telstra Corporation](http://www.telstra.com.au/business-enterprise/network-services/networks/cloud-direct-connect/)** |サポートされています |サポートされています |メルボルン、シドニー |
| **[Telus](http://www.telus.com)** |サポートされています |サポートされています |トロント |
| **[Verizon](http://www.verizonenterprise.com/products/networking/secure-cloud-interconnect/)** |サポートされています |サポートの有無 |アムステルダム、シカゴ、ダラス、香港、ロンドン、シリコン バレー、シンガポール、シドニー、東京、ワシントン DC |
| **[Vodafone](http://www.vodafone.com/business/global-enterprise/global-connectivity/vodafone-ip-vpn-cloud-connect)** |サポートされています |サポートされていません |ロンドン |
| **[Zayo Group](http://www.zayo.com/solutions/industries/cloud-connectivity/microsoft-expressroute)** |サポートされています |サポートされています |シカゴ、ダラス+、ロンドン+、ロサンゼルス、ニューヨーク、シリコン バレー、トロント、ワシントン DC |

 **+** は近日対応予定を表します

### <a name="national-cloud-environment"></a>各国のクラウド環境

### <a name="us-government-cloud"></a>米国政府のクラウド
| **サービス プロバイダー** | **Microsoft Azure** | **Office 365** | **場所** |
| --- | --- | --- | --- |
| **[AT&T NetBond](https://www.synaptic.att.com/clouduser/html/productdetail/ATT_NetBond.htm)** |サポートされています |サポートされています |シカゴ、ワシントン DC |
| **[Equinix](http://www.equinix.com/partners/microsoft-azure/)** |サポートされています |サポートされています |シカゴ、ダラス、ニューヨーク、シアトル、シリコン バレー、ワシントン DC |
| **[Level 3 Communications](http://your.level3.com/LP=882?WT.tsrc=02192014LP882AzureVanityAzureText)** |サポートされています |サポートされています |シカゴ、ニューヨーク+、ワシントン DC |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |サポートされています | サポートされています | シカゴ、ダラス |
| **[Verizon](http://news.verizonenterprise.com/2014/04/secure-cloud-interconnect-solutions-enterprise/)** |サポートされています |サポートされています |シカゴ、ダラス、ニューヨーク、ワシントン DC |

### <a name="china"></a>中国
| **サービス プロバイダー** | **Microsoft Azure** | **Office 365** | **場所** |
| --- | --- | --- | --- |
| **China Telecom** |サポートされています |サポートされていません |北京、上海 |

詳細については、 [中国の ExpressRoute](http://www.windowsazure.cn/home/features/expressroute/)に関するページを参照してください。

### <a name="germany"></a>ドイツ
| **サービス プロバイダー** | **Microsoft Azure** | **Office 365** | **場所** |
| --- | --- | --- | --- |
| **[Colt](http://www.colt.net/uk/en/news/colt-announces-dedicated-cloud-access-for-microsoft-azure-services-en.htm)** |サポートされています |サポートされていません |ベルリン+、フランクフルト |
| **[Equinix](http://www.equinix.com/partners/microsoft-azure/)** |サポートされています |サポートされていません |フランクフルト |
| **[e-shelter](https://www.e-shelter.de/en/microsoft-expressroutetm)** |サポートされています |サポートされていません |ベルリン |
| **Interxion** |サポートされています |サポートされていません |フランクフルト |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |サポートされています  | サポートされていません | ベルリン |

## <a name="connectivity-through-exchange-providers"></a>Exchange プロバイダー経由の接続

接続プロバイダーが上記のセクションの一覧にない場合でも、接続を作成できます。

* 接続プロバイダーが上の表に記載されているいずれかの Exchange に接続されているかどうかをその接続プロバイダーに確認します。 次のリンクから、Exchange プロバイダーが提供するサービスの詳細情報を収集できます。 一部の接続プロバイダーは既にイーサネット Exchange に接続されています。
  * [Cologix](http://www.cologix.com/)
  * [CoreSite](http://www.coresite.com/)
  * [Equinix Cloud Exchange](http://www.equinix.com/services/interconnection-connectivity/cloud-exchange/)
  * [Interxion](http://www.interxion.com/products/interconnection/cloud-connect/)
  * [Megaport](https://www.megaport.com/services/microsoft-expressroute/)
  * [NextDC](http://www.nextdc.com/)
  * [TeleCity CloudIX](http://www.telecitygroup.com/colocation-services/cloud-ix.htm)
* その接続プロバイダーに、選択したピアリングの場所までネットワークを拡張してもらいます。
  * 単一障害点がないように、接続プロバイダーが可用性の高い方法で接続を拡張していることを確認します。
* Microsoft に接続するために、接続プロバイダーとしてその Exchange で ExpressRoute 回線を要求します。
  * 「 [ExpressRoute 回線の作成](expressroute-howto-circuit-classic.md) 」の手順に従い、接続を構築します。

## <a name="connectivity-through-additional-service-providers"></a>追加のサービス プロバイダー経由の接続

| **接続プロバイダー** | **Exchange** | **場所** |
| --- | --- | --- |
| **[1CLOUDSTAR](http://www.1cloudstar.com/service/cloudconnect-azure-expressroute/)** |Equinix |シンガポール |
| **[Airgate Technologies, Inc.](http://airgate.ca/cloud-express/)** | Equinix、Cologix | トロント、モントリオール |
| **[Alaska Communications](http://www.alaskacommunications.com/For-Your-Business/Direct-Cloud-Service)** |Equinix |シアトル |
| **[アルテリア・ネットワークス株式会社](https://arteria-net.com/business/service/cloud_access/sca/)** |Equinix |東京 |
| **[Bezeq International Ltd.](https://www.bezeqint.net/english)** | euNetworks | ロンドン |
| **[C3ntro Telecom](http://www.c3ntro.com/data/cloud-conectivity/)** | Equinix、Megaport | ダラス |
| **[Cogeco Peer 1](https://www.cogecopeer1.com/en/)**| Equinix | モントリオール、トロント |
| **[Cox Business](https://www.cox.com/business/networking/cloud-connectivity.html)** | Equinix | ダラス、シリコン バレー、ワシントン DC | 
| **[Data Foundry](https://www.datafoundry.com/services/cloud-connect)** | Megaport | ダラス |
| **[Epsilon Telecommunications Limited](http://www.epsilontel.com/data-connectivity/cloud-access/)** | Equinix | ロンドン、シンガポール、ワシントン DC |
| **[Eurofiber](https://eurofiber.nl/microsoft-azure/)** | Equinix | アムステルダム |
| **[Exponential E](http://www.exponential-e.com/services/connectivity-services/cloud-connect-exchange)** | Equinix | ロンドン |
| **[Fastweb S.p.A](http://www.fastweb.it/grandi-aziende/connessione-voce-e-wifi/scheda-prodotto/rete-privata-virtuale/)** | Equinix | アムステルダム |
| **[HSO](http://www.hso.co.uk/products/cloud-direct)** |Equinix | ロンドン、スラウ |
| **[Lightower](http://www.lightower.com/network-solutions/cloud-connect/#microsoft-azure)** |Equinix |ニューヨーク、ワシントン DC |
| **[Macquarie Telecom Group](https://macquariegovernment.com/secure-cloud/secure-cloud-exchange/)** | Megaport | シドニー |
| **[Masergy](https://www.masergy.com/solutions/hybrid-networking/cloud-marketplace/microsoft-azure)** | Equinix | ワシントン DC |
| **[NexGen Networks](http://www.nexgen-net.com/nexgen-networks-direct-connect-microsoft-azure-expressroute.html)** | Interxion | ロンドン |
| **[Nianet](https://nianet.dk/produkter/internet/microsoft-expressroute)** |Telecity | アムステルダム、フランクフルト |  
| **[QSC AG](https://www.qsc.de/de/produkte-loesungen/cloud-services-und-it-outsourcing/pure-enterprise-cloud/multi-cloud-management/azure-expressroute/)** |Interxion | フランクフルト |  
| **Rogers** | Cologix、Equinix | モントリオール、トロント |
| **[Tamares Telecom](http://www.tamarestelecom.com/our-services/#Connectivity)** | Telecity | ロンドン | 
| **[ThinkTel](http://www.thinktel.ca/services/agile-ix-data/expressroute/)** | Equinix | トロント | 
| **[Transtelco](http://www.transtelco.net/tcloud/microsoft)** |Equinix | ダラス、ロサンゼルス |  
| **[Webair](https://www.webair.com/microsoft-express-route-partnership/)**| Megaport | ニューヨーク |
| **[Windstream](http://www.windstreambusiness.com/solutions/cloud-services/cloud-and-managed-hosting-services)**| Equinix | シカゴ、シリコン バレー、ワシントン DC |
| **[Zertia](http://www.zertia.es/index.php/novedades)**| レベル 3 | マドリッド |

## <a name="connectivity-through-datacenter-providers"></a>データセンター プロバイダー経由の接続
| **プロバイダー** | **Exchange** |
| --- | --- |
| **[Cyrus One](https://cyrusone.com/enterprise-data-center-services/connectivity-and-interconnection/)** | Megaport |
| **[Digital Realty](https://www.digitalrealty.com/services/interconnection/service-exchange/)** | Megaport |
| **[EdgeConnex](http://www.edgeconnex.com/services/edge-data-centers-proximity-matters/)** | Megaport |

## <a name="connectivity-through-national-research-and-education-networks-nren"></a>国立研究教育ネットワーク (NREN) 経由の接続

| **プロバイダー**|
| --- |
| **AARNET**| 
| **GARR、GÉANT 経由**|
| **GÉANT**|
| **HEAnet、GÉANT 経由**|
| **JISC**|
| **RedIRIS、GÉANT 経由**|
| **Surfnet、GÉANT 経由**|

* ご利用の接続プロバイダーがこの一覧にない場合は、そのプロバイダーが上に記載されている ExpressRoute Exchange パートナーに接続されているかどうかを確認してください。

## <a name="expressroute-system-integrators"></a>ExpressRoute システム インテグレーター
ネットワークの規模によっては、ニーズに合わせてプライベート接続を有効にするのは難しい場合があります。 次の表のいずれかのシステム インテグレーターを使用すると、ExpressRoute の利用開始に役立ちます。

| **システム インテグレーター** | **大陸** |
| --- | --- |
| **[Altogee](http://www.altogee.be/expressroute)** | ヨーロッパ |
| **[Avanade Inc.](http://www.avanade.com/)** | アジア、ヨーロッパ、北米、南アメリカ |
| **[Bright Skies GmbH](http://bskies.io/expressroute)** | ヨーロッパ
| **[Ensyst](http://www.ensyst.com.au)** | アジア
| **[Equinix Professional Services](http://www.equinix.com/services/consulting/)** | 北米 |
| **[The IT Consultancy Group](http://itconsult.com.au/microsoft-expressroute)** | オーストラリア |
| **[MSG Services](https://www.msg-services.de/it-services/managed-services/cloud-outsourcing/)** | ヨーロッパ (ドイツ) |
| **[Nelite](http://nelite.com/)** | ヨーロッパ |
| **[New Signature](https://www.newsignature.co.uk/)** | ヨーロッパ |
| **[OneAs1a](http://www.oneas1a.com/express-connect-any-cloud-ecac)** | アジア |
| **[Orange Networks](https://orange-networks.com/blog/88-azureexpressroute)** | ヨーロッパ |
| **[Perficient](http://www.perficient.com/Partners/Microsoft/Cloud/Azure-ExpressRoute)** | 北米 |
| **[Presidio](http://info.presidio.com/microsoft-azure-expressroute)** | 北米 |
| **[Project Leadership](http://www.projectleadership.net/azure)** | 北米 |
| **[sol-tec](http://www.sol-tec.com/Technologies)** | ヨーロッパ |
| **[Vigilant.IT](https://vigilant.it/expressroute)** | オーストラリア |


## <a name="next-steps"></a>次のステップ
* ExpressRoute の詳細については、「 [ExpressRoute のFAQ](expressroute-faqs.md)」をご覧ください。
* すべての前提条件を満たしていることを確認します。 「 [Azure ExpressRoute の前提条件](expressroute-prerequisites.md)」を参照してください。

<!--Image References-->
[0]: ./media/expressroute-locations/expressroute-locations-map.png "場所のマップ"

