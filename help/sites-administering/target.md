---
title: Adobe Target との統合
description: Adobe Experience ManagerとAdobe Targetを統合する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2b17d8cd-a43c-4d54-b990-a6f0cb1db22b
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 73%

---

# Adobe Target との統合{#integrating-with-adobe-target}

Adobe Marketing Cloud に含まれている [Adobe Target](https://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) を使用すると、あらゆるチャネルにわたってターゲット設定と測定を行い、コンテンツの関連性を高めることができます。Adobe Target はマーケター向けのツールで、オンラインテストを設計および実行し、その場で（行動に基づいた）オーディエンスセグメントを作成し、コンテンツとオンラインエクスペリエンスのターゲット設定を自動化するために使用されます。AEMでは、Adobe Target Standard で使用されるターゲティングワークフローが採用されています。 Target を使用すると、AEM のターゲット設定の編集環境に慣れ親しむことができます。

AEM Sites を Adobe Target に統合して、ページ内のコンテンツを次のようにパーソナライズできます。

* コンテンツのターゲティングを実装します。
* Target のオーディエンスを使用してパーソナライズされたエクスペリエンスを作成する。
* 訪問者がページとやり取りを行ったときにコンテキストデータを Target に送信する。
* コンバージョン率をトラックします。

Target に統合するには、次のタスクを実行します。

1. [前提条件のタスクを実行する](/help/sites-administering/target-requirements.md)：Adobe Target に登録して AEM オーサーインスタンスの特定の側面を設定します。Adobe Target アカウントには、承認者レベル以上の権限が必要です。さらに、ユーザーがアクセスできないように、パブリッシュノードのアクティビティ設定を保護する必要があります。

1. 以下のどちらかの操作を行います。

   1. [Adobe Targetのオプトイン](/help/sites-administering/opt-in.md)：オプトインウィザードは、Target のアカウント情報を取得し、Adobe Targetクラウド設定と Target フレームワークを作成します。 また、このウィザードはサイトを Target フレームワークに関連付けます。 ウィザードが Target に接続できない場合は、 [接続障害発生](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) 」セクションに入力します。 次の操作が可能です。 [デフォルトのクラウド設定を変更する](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations)：必要に応じて、オプトインウィザードで作成したクラウド設定とフレームワークを変更します。 例えば、追加のコンテキストデータを Target に送信するようにフレームワークを変更します。 Adobe AnalyticsをAdobe Targetのレポートソースとして使用する場合は、A4T 設定を指すようにクラウド設定を変更する必要があります。
   1. [手動での Adobe Target との統合](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)

1. [アクティビティを設定する](/help/sites-authoring/activitylib.md)：アクティビティを Target のクラウド設定に関連付けます。

>[!NOTE]
>
>[DTM を使用した AEM と Adobe Target および Adobe Analytics の統合（英語）](https://helpx.adobe.com/jp/experience-manager/using/integrate-digital-marketing-solutions.html)も参照してください。

>[!NOTE]
>
>カスタムプロキシ設定で Target を使用している場合、AEM には 3.x API を使用する機能と 4.x API を使用する機能があるので、両方の HTTP クライアントプロキシを設定する必要があります。
>
>* 3.x は [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) のように設定します。
>* 4.x は [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) のように設定します。
>

>[!CAUTION]
>
>パブリッシュインスタンスでアクティビティ設定ノード **cq:ActivitySettings** を保護し、通常のユーザーがアクセスできないようにします。アクティビティ設定ノードには、Adobe Target へのアクティビティの同期を処理するサービスのみがアクセスできるようにしてください。
>
>詳しくは、[Adobe Target との統合の前提条件](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node)を参照してください。

統合が完了したら、訪問者データを Adobe Target に送信する[ターゲットコンテンツを作成](/help/sites-authoring/content-targeting-touch.md)できます。コンテンツのターゲティングを有効にするには、ページのコンポーネントに固有のコードが必要です( 詳しくは、 [ターゲットコンテンツ用の開発](/help/sites-developing/target.md).)

>[!NOTE]
>
>AEM オーサーインスタンスでコンポーネントをターゲット設定すると、そのコンポーネントが、キャンペーンの登録、オファーの設定、Adobe Target セグメントの取得（設定されている場合）を行うために、Adobe Target に対して一連のサーバー側呼び出しを実行します。AEM パブリッシュから Adobe Target にサーバー側呼び出しは作成されません。

## 背景情報ソース {#background-information-sources}

AEMとAdobe Targetの統合には、Adobe Target、AEMアクティビティの管理、AEM Audiences の管理に関する知識が必要です。 以下を十分理解している必要があります。

* Adobe Target（[Adobe Target のドキュメント](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=ja)を参照）
* AEM アクティビティコンソール（[アクティビティの管理](/help/sites-authoring/activitylib.md)を参照）。
* AEM オーディエンス（[オーディエンスの管理](/help/sites-authoring/managing-audiences.md)を参照）。

>[!NOTE]
>
>Adobe Target を操作する場合、1 つのキャンペーンで許可されるアーティファクトの最大数は次のとおりです。
>
>* 場所：50
>* エクスペリエンス：2,000
>* 指標：50
>* レポートセグメント：50
>
