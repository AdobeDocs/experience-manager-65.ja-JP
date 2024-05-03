---
title: Correspondence Management | ユーザーデータの処理
description: Adobe Experience Manager Forms 環境での Correspondence Management とユーザーデータの処理について説明します。
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: a0c6a02c-47a3-4e70-a14c-953ee016b8e4
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 100%

---

# Correspondence Management | ユーザーデータの処理 {#correspondence-management-handling-user-data}

AEM Forms Correspondence Management を使用すると、安全でパーソナライズされた顧客対応を作成、管理、合理化できます。ビジネスユーザー向けに直感的なユーザーインターフェイスを提供し、事前に承認されたコンテンツブロックとメディア要素を使用して通信を作成できるようにします。通信の作成について詳しくは、[通信の作成](/help/forms/using/create-correspondence.md)を参照してください。

ビジネスユーザーまたはエージェントが通信をドラフトとして格納したり送信したりする場合、レターインスタンスが AEM リポジトリに格納されます。レターインスタンスには、通信データとメタデータが含まれます。

>[!NOTE]
>
>AEM 6.5 Forms では、通信の管理は初期状態では使用できません。以前のバージョンの AEM Forms からアップグレードする場合は、互換性パッケージをインストールして Correspondence Management のアセットを移行し、AEM 6.5 Forms で引き続き使用できるようにします。詳しくは、[互換パッケージ](/help/forms/using/compatibility-package.md)を参照してください。

## ユーザーデータとデータストア {#data}

Correspondence Management では、パブリッシュインスタンスがレターインスタンスを管理するように設定されている場合にのみ、ドラフトおよび送信済みレターのデータが AEM リポジトリに格納されます。この設定について詳しくは、[Correspondence Management 設定プロパティ](/help/forms/using/cm-configuration-properties.md)を参照してください。

AEM デプロイメント用に設定されたデータストアの永続性に応じて、ドラフトおよび送信済み通信データは次の場所に格納されます。

<table>
 <tbody>
  <tr>
   <td><p><strong>永続性タイプ</strong></p> </td>
   <td><p><strong>データストア</strong></p> </td>
   <td><p><strong>場所</strong></p> </td>
  </tr>
  <tr>
   <td><p>デフォルト</p> </td>
   <td><p>リバースレプリケーション設定で指定されたパブリッシュインスタンスおよびオーサーインスタンスの AEM リポジトリ</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code><br /> </p> </td>
  </tr>
  <tr>
   <td><p>リモート</p> </td>
   <td><p>オーサーインスタンスを処理するリモートの AEM リポジトリ</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

上記の AEM リポジトリの場所で：

* `[yyyy]/[mm]/[dd]` は、レターインスタンスが作成された日付にもとづいたノード構成を示します。
* `[node-id]` は、レターを含むフォルダーに割り当てられた ID を示します。
* `[letter-instance-name]` は、レターを保存または送信したときに指定された名前を示します。

[letter-instance-name] ノードでは以下のノード構造が作成され、各レターインスタンスのデータが AEM リポジトリに格納されます。

| ノード | 説明 |
|---|---|
| `extendedProperties` | レターインスタンスのメタデータのプロパティを格納します。 |
| `dataXML` | 通信データを含むダウンロード可能な dataXML ファイルをバイナリ形式で格納します。 |
| `processedXDP` | 送信済みレターを作成するために使用される XDP テンプレートの詳細が含まれています。このノードは、送信された通信に対してのみ作成されます。 |
| `submittedLetter` | 送信済みレターデータをダウンロード可能なバイナリ形式で格納します。このノードは、送信された通信に対してのみ作成されます。 |

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

設定されたデータストアのドラフトおよび送信済み通信データにアクセスし、必要に応じて削除することができます。

### ユーザーデータにアクセス {#access-user-data}

Correspondence Management には、ドラフトおよび送信済みレターインスタンスを検索してアクセスするために使用できる API が用意されています。API を使用すると、レターインスタンス ID または通信を保存または送信したユーザーを使用して、レターインスタンスを検索して開くことができます。詳しくは、[レターインスタンスにアクセスするための API](/help/forms/using/cm-apis-to-access-letter-instances.md) を参照してください。

または、CRXDE Lite を使用して AEM リポジトリのレターインスタンスに移動することもできます。格納されたデータおよびリポジトリの場所について詳しくは、[ユーザーデータとデータストア](/help/forms/using/correspondence-management-handling-user-data.md#data)を参照してください。

### ユーザーデータの削除 {#delete-user-data}

特定ユーザーのデータを含むレターインスタンスを検索するには、次の操作を実行します。

* レターインスタンス名、ドラフトを保存したユーザー、または通信を送信したユーザーがわかっている場合は、Correspondence Management API を使用します
* メール ID や名前など、個人を特定できる情報を使用して AEM リポジトリを検索し、情報が格納されているノードを探します

AEM システムでドラフトおよび送信済み通信に含まれるユーザーデータを完全に削除するには、適用可能なすべての AEM インスタンスからレターインスタンスノードを手動で削除する必要があります。
