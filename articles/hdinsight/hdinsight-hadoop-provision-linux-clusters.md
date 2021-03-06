﻿---
title: "Azure HDInsight での Hadoop、HBase、Kafka、Storm、または Spark クラスターの作成 | Microsoft Docs"
description: "ブラウザー、Azure CLI、Azure PowerShell、REST、または SDK を使用して HDInsight に Linux ベースの Hadoop、HBase、Storm、または Spark クラスターを作成する方法について説明します。"
keywords: "Hadoop クラスターのセットアップ, Kafka クラスターのセットアップ, Spark クラスターのセットアップ, HBase クラスターのセットアップ, Storm クラスターのセットアップ, Hadoop のクラスターとは"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 23a01938-3fe5-4e2e-8e8b-3368e1bbe2ca
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: jgao
ms.translationtype: Human Translation
ms.sourcegitcommit: 5e92b1b234e4ceea5e0dd5d09ab3203c4a86f633
ms.openlocfilehash: ed0a5cfc02572d537f4b179ad612ad153a2db1d4
ms.contentlocale: ja-jp
ms.lasthandoff: 05/10/2017


---
# <a name="create-hadoop-clusters-in-hdinsight"></a>HDInsight で Hadoop クラスターを作成する
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Hadoop クラスターは、クラスターでのタスクの分散処理に使用される複数の仮想マシン (ノード) で構成されます。 Azure HDInsight では、個々のノードのインストールと構成の実装の詳細を抽象化しているため、提供する必要があるのは一般的な構成情報のみとなります。 この記事では、これらの構成設定について説明します。

## <a name="basic-configurations"></a>基本構成

[Azure Portal](https://portal.azure.com) から、 *[簡易作成]* または *[カスタム]* を使用して、HDInsight クラスターを作成できます。 このセクションでは、[簡易作成] オプションで使用する基本的な構成設定について説明します。 [カスタム] オプションには、次の追加の構成が含まれています。

- [アプリケーション](#hdinsight-applications)
- [クラスター サイズ](#cluster-size)
- 詳細設定

  - [スクリプト アクション](#customize-clusters-using-script-action)
  - [Virtual Network](#use-virtual-network)

### <a name="subscription"></a>[サブスクリプション] 
各 HDInsight クラスターは、1 つの Azure サブスクリプションに関連付けられます。

### <a name="resource-group-name"></a>リソース グループ名
[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) を使用すると、アプリケーション内の複数のリソースを、Azure リソース グループと呼ばれる 1 つのグループとして使用できます。 アプリケーションのこれらすべてのリソースを、1 回の連携した操作でデプロイ、更新、監視、または削除できます。

### <a name="cluster-name"></a>クラスター名
クラスター名は、クラスターの識別に使用します。 クラスター名はグローバルに一意である必要があり、次の名前付けのガイドラインに従う必要があります。

* このフィールドには、3 ～ 63 文字の文字列を指定する必要があります。
* このフィールドには、文字、数字、ハイフンのみを含めることができます。

### <a name="cluster-types"></a>クラスターの種類
現在、Azure HDInsight では、以下の種類のクラスターを提供しています。それぞれのクラスターは特定の機能を提供する一連のコンポーネントを備えています。

| クラスターの種類 | 機能 |
| --- | --- |
| [Hadoop](hdinsight-hadoop-introduction.md) |クエリと分析 (バッチ ジョブ) |
| [HBase](hdinsight-hbase-overview.md) |NoSQL データ ストレージ |
| [Storm](hdinsight-storm-overview.md) |リアルタイム イベント処理 |
| [Spark](hdinsight-apache-spark-overview.md) |メモリ内処理、対話型クエリ、マイクロバッチ ストリーム処理 |
| [Kafka (プレビュー)](hdinsight-apache-kafka-introduction.md) | リアルタイムのストリーミング データ パイプラインとアプリケーションの構築に使用できる分散ストリーム プラットフォーム |
| [R Server](hdinsight-hadoop-r-server-overview.md) |さまざまなビッグ データ統計、予測モデリング、機械学習の機能 |
| [対話型 Hive (プレビュー)](hdinsight-hadoop-use-interactive-hive.md) |対話型で高速な Hive クエリのメモリ内キャッシュ |

各クラスターの種類には、クラスター内の独自のノード数、クラスター内のノードを表す用語、およびノードの種類ごとに既定の VM サイズがあります。 次の表では、各ノードの種類のノード数がかっこ内に示されています。

| 型 | Nodes | ダイアグラム |
| --- | --- | --- |
| Hadoop は、 |ヘッド ノード (2)、データ ノード (1 以上) |![HDInsight Hadoop クラスター ノード](./media/hdinsight-hadoop-provision-linux-clusters/HDInsight-Hadoop-roles.png) |
| HBase |ヘッド サーバー (2)、リージョン サーバー (1 以上)、マスター/ZooKeeper ノード (3) |![HDInsight HBase クラスター ノード](./media/hdinsight-hadoop-provision-linux-clusters/HDInsight-HBase-roles.png) |
| Storm |Nimbus ノード (2)、Supervisor サーバー (1 以上)、ZooKeeper ノード (3) |![HDInsight Storm クラスター ノード](./media/hdinsight-hadoop-provision-linux-clusters/HDInsight-Storm-roles.png) |
| Spark |ヘッド ノード (2)、ワーカー ノード (1 以上)、ZooKeeper ノード (3) (A1 ZooKeeper VM サイズでは無料) |![HDInsight Spark クラスター ノード](./media/hdinsight-hadoop-provision-linux-clusters/HDInsight-Spark-roles.png) |

次の表に、HDInsight の既定の VM サイズを示します。

* ブラジル南部と西日本を除くすべてのサポートされているリージョン:

  | クラスターの種類 | Hadoop は、 | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | ヘッド: 既定の VM サイズ |D3 v2 |D3 v2 |A3 |D12 v2 |D12 v2 |
  | ヘッド: 推奨される VM サイズ |D3 v2、D4 v2、D12 v2 |D3 v2、D4 v2、D12 v2 |A3、A4、A5 |D12 v2、D13 v2、D14 v2 |D12 v2、D13 v2、D14 v2 |
  | worker: 既定の VM サイズ |D3 v2 |D3 v2 |D3 v2 |Windows: D12 v2、Linux: D4 v2 |Windows: D12 v2、Linux: D4 v2 |
  | worker: 推奨される VM サイズ |D3 v2、D4 v2、D12 v2 |D3 v2、D4 v2、D12 v2 |D3 v2、D4 v2、D12 v2 |Windows: D12 v2、D13 v2、D14 v2、Linux: D4 v2、D12 v2、D13 v2、D14 v2 |Windows: D12 v2、D13 v2、D14 v2、Linux: D4 v2、D12 v2、D13 v2、D14 v2 |
  | ZooKeeper: 既定の VM サイズ | |A3 |A2 | | |
  | ZooKeeper: 推奨される VM サイズ | |A3、A4、A5 |A2、A3、A4 | | |
  | エッジ: 既定の VM サイズ | | | | |Windows: D12 v2、Linux: D4 v2 |
  | エッジ: 推奨される VM サイズ | | | | |Windows: D12 v2、D13 v2、D14 v2、Linux: D4 v2、D12 v2、D13 v2、D14 v2 |
* ブラジル南部と西日本のみ (v2 サイズはありません):

  | クラスターの種類 | Hadoop は、 | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | ヘッド: 既定の VM サイズ |D3 |D3 |A3 |D12 |D12 |
  | ヘッド: 推奨される VM サイズ |D3、D4、D12 |D3、D4、D12 |A3、A4、A5 |D12、D13、D14 |D12、D13、D14 |
  | worker: 既定の VM サイズ |D3 |D3 |D3 |Windows: D12、Linux: D4 |Windows: D12、Linux: D4 |
  | worker: 推奨される VM サイズ |D3、D4、D12 |D3、D4、D12 |D3、D4、D12 |Windows: D12、D13、D14、Linux: D4、D12、D13、D14 |Windows: D12、D13、D14、Linux: D4、D12、D13、D14 |
  | ZooKeeper: 既定の VM サイズ | |A2 |A2 | | |
  | ZooKeeper: 推奨される VM サイズ | |A2、A3、A4 |A2、A3、A4 | | |
  | エッジ: 既定の VM サイズ | | | | |Windows: D12、Linux: D4 |
  | エッジ: 推推奨される VM サイズ | | | | |Windows: D12、D13、D14、Linux: D4、D12、D13、D14 |

> [!NOTE]
> ヘッドは、Storm クラスター タイプでは *Nimbus* と呼ばれます。 worker は、HBase クラスターでは *"リージョン"*、Storm クラスターでは *"スーパーバイザー"* と呼ばれます。

> [!IMPORTANT]
> クラスターの作成時または作成後のスケーリングで 32 個を超えるワーカー ノードを使用することを予定している場合は、コア数が 8 個以上、RAM が 14 GB 以上のヘッド ノード サイズを選択する必要があります。
>
>

[スクリプト アクション](#customize-clusters-using-script-action)を使用すると、これらの基本的な種類に Hue などの他のコンポーネントを追加できます。

> [!IMPORTANT]
> HDInsight クラスターには、ワークロード、またはクラスターが調整されるテクノロジに対応するさまざまな型があります。 1 つのクラスターの Storm と HBase など、複数の種類を結合するクラスターを作成するメソッドはサポートされていません。
>
>

ソリューションに複数の HDInsight クラスターの種類に分散されたテクノロジが必要な場合は、Azure の仮想ネットワークを作成し、その仮想ネットワーク内で必要なクラスターの種類を作成する必要があります。 この構成により、クラスターと、それにデプロイするすべてのコードが互いに通信できるようになります。

Azure の仮想ネットワークの HDInsight との併用の詳細については、[Azure の仮想ネットワークを使用した HDInsight 機能の拡張](hdinsight-extend-hadoop-virtual-network.md)に関するページをご覧ください。

Azure の仮想ネットワーク内で 2 つのクラスターの種類を使用した例の詳細については、[Storm と HBase を使用したセンサー データの分析](hdinsight-storm-sensor-data-analysis.md)に関するページをご覧ください。

### <a name="operating-system"></a>オペレーティング システム
HDInsight クラスターは、Linux と Windows のいずれかで作成できます。  OS のバージョンの詳細については、「[サポートされる HDInsight のバージョン](hdinsight-component-versioning.md#supported-hdinsight-versions)」を参照してください。 HDInsight 3.4 以降では、クラスターを作成する OS として、Ubuntu Linux ディストリビューションを使用します。 

### <a name="version"></a>バージョン
このオプションを使用して、このクラスターに必要な HDInsight のバージョンを指定します。 詳細については、「[サポートされる HDInsight のバージョン](hdinsight-component-versioning.md#supported-hdinsight-versions)」を参照してください。

### <a name="cluster-tiers"></a>クラスター レベル

Azure HDInsight では、Standard と Premium の 2 つのカテゴリでビッグ データ クラウド サービスを提供します。  詳細については、「HDInsight Standard と HDInsight Premium」(hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium) を参照してください。

次のスクリーンショットは、クラスターの種類を選択するための Azure ポータルの情報を示しています。

![HDInsight Premium の構成](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


### <a name="credentials"></a>資格情報
HDInsight クラスターでは、クラスターの作成時に次の 2 つのユーザー アカウントを構成できます。

* HTTP ユーザー。 既定のユーザー名は *admin* です。 Azure Portal の基本的な構成を使用します。 "クラスター ユーザー" と呼ばれることもあります。
* SSH ユーザー (Linux クラスター)。 SSH 経由でクラスターに接続する際に使用します。 詳細については、[HDInsight での SSH の使用](hdinsight-hadoop-linux-use-ssh-unix.md)に関するページを参照してください。

### <a name="location"></a>場所
クラスターの場所を明示的に指定する必要はありません。 クラスターは、既定のストレージの場所を共有します。 サポートされているリージョンのリストについては、「 **HDInsight の価格** 」の [[リージョン]](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409)ドロップダウン リストをクリックしてください。


### <a name="storage"></a>Storage

元の Hadoop 分散ファイル システム (HDFS) は、クラスター上の多数のローカル ディスクを使用します。 HDInsight では、[Azure Storage](hdinsight-hadoop-provision-linux-clusters.md#azure-storage) または [Azure Data Lake Store](hdinsight-hadoop-provision-linux-clusters.md#azure-data-lake-store) の BLOB が使用されます。 HDInsight で Data Lake Store を使用するには、特定の要件を満たす必要があります。 詳細については、「[Azure Portal を使用して、Data Lake Store を使用する HDInsight クラスターを作成する](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)」の冒頭部分を参照してください。

![HDInsight ストレージ](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)


#### <a name="azure-storage"></a>Azure Storage
Azure Storage は、堅牢な汎用ストレージ ソリューションであり、HDInsight とシームレスに統合されます。 HDInsight のすべてのコンポーネントは、BLOB に格納された構造化データまたは非構造化データを HDFS インターフェイスを介して直接操作できます。 Azure Storage にデータを格納すると、ユーザー データを失わずに、計算に使用されている HDInsight クラスターを安全に削除できます。 __汎用__の Azure Storage アカウントがサポートされるのは HDInsight のみです。 現時点では、__Blob Storage__ タイプのアカウントはサポートされません。

構成時に、Azure Storage アカウントと、その Azure Storage アカウントの BLOB コンテナーを指定します。 BLOB コンテナーは、既定の保存先としてクラスターで使用されます。 必要に応じて、クラスターがアクセスできるその他の Azure Storage アカウント (リンクされたストレージ) を指定できます。 クラスターは、完全なパブリック読み取りアクセスまたは BLOB のみを対象とするパブリック読み取りアクセスで構成された BLOB コンテナーにアクセスすることもできます。

ビジネス データの格納には、既定の BLOB コンテナーを使用しないことをお勧めします。 ストレージ コストを削減するために、既定の BLOB コンテナーの使用後、コンテナーを毎回削除することをお勧めします。 既定のコンテナーには、アプリケーション ログとシステム ログが格納されます。 コンテナーを削除する前に、ログを取り出してください。

1 つの BLOB コンテナーを複数のクラスターで共有することはサポートされていません。

Azure Storage アカウントの使用方法の詳細については、「[HDInsight での Azure Storage の使用](hdinsight-hadoop-use-blob-storage.md)」を参照してください。

#### <a name="azure-data-lake-store"></a>Azure Data Lake Store
Azure Storage に加え、[Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md) が、HDInsight での HBase クラスターの既定のストレージ アカウントとして、4 種類すべての HDInsight クラスターのリンクされたストレージとして使用できます。 詳細については、「 [Azure ポータルを使用して、Data Lake Store を使用する HDInsight クラスターを作成する](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)」を参照してください。

#### <a name="use-additional-storage"></a>その他のストレージ

場合によっては、クラスターへのストレージの追加が必要になることがあります。 たとえば、異なる地理的リージョンまたは異なるサービスの複数の Azure ストレージ アカウントがあり、それらをすべて HDInsight で分析する場合などです。

HDInsight クラスターを作成するとき、あるいはクラスターが作成された後に、ストレージ アカウントを追加できます。  「 [スクリプト アクションを使用して Linux ベースの HDInsight クラスターをカスタマイズする](hdinsight-hadoop-customize-cluster-linux.md)」をご覧ください。

セカンダリ Azure Storage アカウントの詳細については、[HDInsight での Azure Storage の使用](hdinsight-hadoop-use-blob-storage.md)に関する記事をご覧ください。 セカンダリ Data Lake Store の詳細については、「 [Azure ポータルを使用して、Data Lake Store を使用する HDInsight クラスターを作成する](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)」をご覧ください。


#### <a name="use-hiveoozie-metastore"></a>Hive metastore

HDInsight クラスターを削除した後も Hive テーブルを保持する場合は、カスタムのメタストアを使用することをお勧めします。 そのメタストアを別の HDInsight クラスターにアタッチすることもできます。

> [!IMPORTANT]
> あるバージョンの HDInsight クラスター用に作成された HDInsight metastore は、別の HDInsight クラスター バージョン間で共有できません。 HDInsight のバージョンの一覧は、「[サポートされる HDInsight のバージョン](hdinsight-component-versioning.md#supported-hdinsight-versions)」をご覧ください。

メタストアには、Hive テーブル、パーティション、スキーマ、列などについての Hive メタデータが格納されます。 メタストアで Hive メタデータを保持できるため、新しいクラスターを作成するときに、Hive テーブルを再作成する必要はありません。 既定では、Hive は組み込みの Azure SQL Database を使用してこの情報を格納します。 組み込みデータベースは、クラスターが削除されるとメタデータを保持できません。 Hive metastore が構成された HDInsight クラスターで Hive テーブルを作成すると、同じ Hive metastore を使用してクラスターを再作成したときにそれらのテーブルが保持されます。

すべてのクラスターの種類で、メタストア構成が使用できるわけではありません。 たとえば、HBase または Kafka クラスターでは使用できません。

> [!IMPORTANT]
> カスタム メタストアを作成するときは、データベース名にダッシュ、ハイフン、またはスペースを使用しないでください。 クラスター作成プロセスが失敗する可能性があります。

> [!WARNING]
> Hive metastore では、Azure SQL Warehouse はサポートされていません。


#### <a name="oozie-metastore"></a>Oozie メタストア

Oozie の使用時にパフォーマンスを向上させるには、カスタム メタストアを使用します。 カスタム メタストアは、クラスターを削除した後に Oozie ジョブ データにアクセスする場合にも役立ちます。 Oozie の使用を予定していない場合、または断続的に Oozie を使用するのみである場合は、カスタム メタストアを作成する必要はありません。

> [!IMPORTANT]
> カスタム Oozie メタストアを再利用することはできません。 カスタム Oozie メタストアを使用するには、HDInsight クラスターの作成時に空の Azure SQL Database を提供する必要があります。

すべてのクラスターの種類で、メタストア構成が使用できるわけではありません。 たとえば、HBase または Kafka クラスターでは使用できません。

> [!WARNING]
> Oozie メタストアでは、Azure SQL Warehouse はサポートされていません。

## <a name="install-hdinsight-applications"></a>HDInsight アプリケーションをインストールする

HDInsight アプリケーションは、ユーザーが Linux ベースの HDInsight クラスターにインストールすることのできるアプリケーションです。 マイクロソフトや独立系ソフトウェア ベンダー (ISV) によって作成されるほか、ユーザーが独自に作成することもできます。 詳細については、「[Azure HDInsight へのサード パーティ製 Hadoop アプリケーションのインストール](hdinsight-apps-install-applications.md)」を参照してください。

HDInsight のアプリケーションのほとんどは、空のエッジ ノードにインストールされます。  空のエッジ ノードは、ヘッド ノードの場合と同じクライアント ツールがインストールされ、構成された Linux 仮想マシンです。 エッジ ノードは、クラスターへのアクセス、クライアント アプリケーションのテスト、およびクライアント アプリケーションのホストに使用できます。 詳細については、「 [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md)」(HDInsight で空のエッジ ノードを使用する) を参照してください。

## <a name="configure-cluster-size"></a>クラスター サイズの構成

クラスターの有効期間中、これらのノードの使用量に対して課金されます。 課金はクラスターが作成されると開始され、クラスターが削除されると停止されます。 クラスターを割り当て解除または保留にすることはできません。

クラスターの種類によって、ノードの種類、ノード数、ノード サイズが異なります。 たとえば、Hadoop クラスターの種類には 2 つの "*ヘッド ノード*" と 4 つの "*データ ノード*" (既定) がありますが、Storm クラスターの種類には 2 つの "*Nimbus ノード*"、3 つの "*ZooKeeper ノード*" と 4 つの "*Supervisor ノード*" (既定) があります。 HDInsight クラスターのコストは、ノード数とノードの仮想マシンのサイズによって決まります。 たとえば、大量のメモリを必要とする操作を実行することがわかっている場合は、より多くのメモリを持つコンピューティング リソースを選択できます。 学習目的の場合は、1 つのデータ ノードを使用することをお勧めします。 HDInsight の価格の詳細については、「 [HDInsight 価格](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409)」をご覧ください。

> [!NOTE]
> クラスター サイズの制限は、Azure サブスクリプションによって異なります。 制限値を上げるには、課金サポートにお問い合わせください。
>
> ノードに使用される仮想マシン イメージは HDInsight サービスの実装の詳細であるため、クラスターで使用されるノードは仮想マシンとしてカウントされません。 ノードで使用されるコンピューティング コアは、サブスクリプションで利用できるコンピューティング コアとしてカウントされ、その合計数に含まれます。 HDInsight クラスターを作成する場合の利用可能なコアの数とクラスターで使用されるコアの数は、**[クラスター サイズ]** ブレードの概要セクションで確認できます。
>
>

Azure Portal を使用してクラスターを構成するときに、**[ノード価格レベル]** ブレードでノード サイズを利用できます。 また、別のノード サイズに関連するコストを確認することもできます。 次のスクリーンショットは、Linux ベースの Hadoop クラスターの選択肢を示しています。

![HDInsight VM ノードのサイズ](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

次の表に、HDInsight クラスターでサポートされているサイズと、それらが提供する容量を示します。

### <a name="standard-tier-a-series"></a>Standard レベル: A シリーズ
クラシック デプロイ モデルでは、一部の VM サイズが PowerShell とコマンド ライン インターフェイス (CLI) で若干異なります。

* Standard_A3: Large
* Standard_A4: ExtraLarge

| サイズ | CPU コア数 | メモリ | NIC (最大) | 最大 ディスク サイズ | 最大 データ ディスク数 (各ディスク 1,023 GB) | 最大 IOPS (各ディスク 500) |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A3\Large |4 |7 GB |2 |一時ディスク = 285 GB |8 |8 x 500 |
| Standard_A4\ExtraLarge |8 |14 GB |4 |一時ディスク = 605 GB |16 |16 x 500 |
| Standard_A6 |4 |28 GB |2 |一時ディスク = 285 GB |8 |8 x 500 |
| Standard_A7 |8 |56 GB |4 |一時ディスク = 605 GB |16 |16 x 500 |

### <a name="standard-tier-d-series"></a>Standard レベル: D シリーズ
| サイズ | CPU コア数 | メモリ | NIC (最大) | 最大 ディスク サイズ | 最大 データ ディスク数 (各ディスク 1,023 GB) | 最大 IOPS (各ディスク 500) |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_D3 |4 |14 GB |4 |一時的 (SSD) = 200 GB |8 |8 x 500 |
| Standard_D4 |8 |28 GB |8 |一時的 (SSD) = 400 GB |16 |16 x 500 |
| Standard_D12 |4 |28 GB |4 |一時的 (SSD) = 200 GB |8 |8 x 500 |
| Standard_D13 |8 |56 GB |8 |一時的 (SSD) = 400 GB |16 |16 x 500 |
| Standard_D14 |16 |112 GB |8 |一時的 (SSD) = 800 GB |32 |32 x 500 |

### <a name="standard-tier-dv2-series"></a>Standard レベル: Dv2 シリーズ
| サイズ | CPU コア数 | メモリ | NIC (最大) | 最大 ディスク サイズ | 最大 データ ディスク数 (各ディスク 1,023 GB) | 最大 IOPS (各ディスク 500) |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_D3_v2 |4 |14 GB |4 |一時的 (SSD) = 200 GB |8 |8 x 500 |
| Standard_D4_v2 |8 |28 GB |8 |一時的 (SSD) = 400 GB |16 |16 x 500 |
| Standard_D12_v2 |4 |28 GB |4 |一時的 (SSD) = 200 GB |8 |8 x 500 |
| Standard_D13_v2 |8 |56 GB |8 |一時的 (SSD) = 400 GB |16 |16 x 500 |
| Standard_D14_v2 |16 |112 GB |8 |一時的 (SSD) = 800 GB |32 |32 x 500 |

これらのリソースの使用を計画するときに注意する必要のあるデプロイの考慮事項については、 [仮想マシンのサイズ](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)に関する記事をご覧ください。 さまざまなサイズの価格については、「[HDInsight の価格](https://azure.microsoft.com/pricing/details/hdinsight)」をご覧ください。   

> [!IMPORTANT]
> クラスターの作成時または作成後のスケーリングで 32 個を超えるワーカー ノードを使用することを予定している場合は、コア数が 8 個以上、RAM が 14 GB 以上のヘッド ノード サイズを選択する必要があります。
>
>

課金はクラスターが作成されると開始され、クラスターが削除されると停止されます。 価格の詳細については、 [HDInsight の価格詳細](https://azure.microsoft.com/pricing/details/hdinsight/)に関する記述を参照してください。


> [!WARNING]
> HDInsight クラスター以外の場所で追加のストレージ アカウントを使用することはできません。



## <a name="use-virtual-network"></a>仮想ネットワークの使用
[Azure Virtual Network](https://azure.microsoft.com/documentation/services/virtual-network/) を使用すると、ソリューションに必要なリソースを含む、セキュリティで保護された永続的なネットワークを作成できます。 仮想ネットワークの具体的な構成要件など、仮想ネットワークで HDInsight を使用する方法の詳細については、「[Azure Virtual Network を使用した HDInsight 機能の拡張](hdinsight-extend-hadoop-virtual-network.md)」をご覧ください。


## <a name="customize-clusters-using-script-action"></a>スクリプト アクションを使用したクラスターのカスタマイズ

追加コンポーネントをインストールするか、作成中にスクリプトを使用してクラスターの構成をカスタマイズできます。 このようなスクリプトは、**スクリプト操作**を使用して実行します。これは Azure ポータル、HDInsight Windows PowerShell コマンドレット、HDInsight .NET SDK で使用できる構成オプションです。 詳しくは、「[Script Action を使って HDInsight をカスタマイズする](hdinsight-hadoop-customize-cluster-linux.md)」をご覧ください。

Mahout や Cascading などの一部のネイティブ Java コンポーネントは、Java アーカイブ (JAR) ファイルとしてクラスター上で実行できます。 これらの JAR ファイルは、Azure Storage に分配し、Hadoop ジョブ送信メカニズムによって HDInsight クラスターに送信できます。 詳細については、 [プログラムによる Hadoop ジョブの送信](hdinsight-submit-hadoop-jobs-programmatically.md)に関するページを参照してください。

> [!NOTE]
> HDInsight クラスターへの JAR ファイルのデプロイ、または HDInsight クラスターでの JAR ファイルの呼び出しに関する問題がある場合は、[Microsoft サポート](https://azure.microsoft.com/support/options/)にお問い合わせください。
>
> Cascading は HDInsight ではサポートされておらず、Microsoft サポートの対象でもありません。 サポートされているコンポーネントの一覧については、[HDInsight で提供されるクラスター バージョンの新機能](hdinsight-component-versioning.md)に関する記事をご覧ください。
>
>

場合によっては、作成プロセス中に次の構成ファイルを設定する必要があります。

* clusterIdentity.xml
* core-site.xml
* gateway.xml
* hbase-env.xml
* hbase-site.xml
* hdfs-site.xml
* hive-env.xml
* hive-site.xml
* mapred-site
* oozie-site.xml
* oozie-env.xml
* storm-site.xml
* tez-site.xml
* webhcat-site.xml
* yarn-site.xml

詳細については、「 [ブートストラップを使って HDInsight クラスターをカスタマイズする](hdinsight-hadoop-customize-cluster-bootstrap.md)」をご覧ください。

## <a name="cluster-creation-methods"></a>クラスターの作成方法
この記事では、Linux ベースの HDInsight クラスターの作成に関する基本的な情報を提供しました。 次の表を使用して、ニーズに最も適した方法を使用したクラスターの作成方法に関する特定の情報を見つけてください。

| クラスターの作成方法 | Web ブラウザー | コマンド ライン | REST API | SDK | Linux、Mac OS X、または Unix | Windows |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| [Azure ポータル](hdinsight-hadoop-create-linux-clusters-portal.md) |✔ |&nbsp; |&nbsp; |&nbsp; |✔ |✔ |
| [Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) |✔ |✔ |✔ |✔ |✔ |✔ |
| [Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |✔ |&nbsp; |&nbsp; |✔ |✔ |
| [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |✔ |&nbsp; |&nbsp; |✔ |✔ |
| [cURL](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |✔ |✔ |&nbsp; |✔ |✔ |
| [.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |✔ |✔ |✔ |
| [Azure リソース マネージャーのテンプレート](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |✔ |&nbsp; |&nbsp; |✔ |✔ |

## <a name="troubleshoot"></a>トラブルシューティング

HDInsight クラスターの作成で問題が発生した場合は、「[アクセス制御の要件](hdinsight-administer-use-portal-linux.md#create-clusters)」を参照してください。

## <a name="next-steps"></a>次のステップ

- [HDInsight とは](hdinsight-hadoop-introduction.md)。
- [Hadoop チュートリアル: HDInsight で Hadoop を使用する](hdinsight-hadoop-linux-tutorial-get-started.md)。
