---
title: Correspondence Management | ユーザーデータの処理
description: AEM Forms環境での Correspondence Management とユーザーデータの処理。
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
role: Admin
exl-id: a0c6a02c-47a3-4e70-a14c-953ee016b8e4
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 45%

---

# Correspondence Management | ユーザーデータの処理 {#correspondence-management-handling-user-data}

AEM Forms Correspondence Management を使用すると、安全でパーソナライズされた顧客通信を作成、管理、合理化できます。 直感的なユーザーインターフェイスを備えており、事前に承認されたコンテンツブロックやメディア要素を使用して通信を作成できます。 通信の作成について詳しくは、[通信の作成](/help/forms/using/create-correspondence.md)を参照してください。

ビジネスユーザーまたはエージェントが通信をドラフトとして保存または送信すると、レターインスタンスがAEMリポジトリに保存されます。 レターインスタンスには、通信データとメタデータが含まれます。

>[!NOTE]
>
>AEM 6.5 Forms では、通信の管理は初期状態では使用できません。以前のバージョンの AEM Forms からアップグレードする場合は、互換性パッケージをインストールして Correspondence Management のアセットを移行し、AEM 6.5 Forms で引き続き使用できるようにします。詳しくは、 [互換性パッケージ](/help/forms/using/compatibility-package.md).

## ユーザーデータとデータストア {#data}

Correspondence Management は、レターインスタンスを管理するようにパブリッシュインスタンスが設定されている場合にのみ、ドラフトおよび送信済みレターのデータをAEMリポジトリに保存します。 設定について詳しくは、 [Correspondence Management 設定プロパティ](/help/forms/using/cm-configuration-properties.md).

AEMのデプロイメント用に設定されたデータストアの永続性に応じて、ドラフトと送信済みの通信データは次の場所に保存されます。

<table>
 <tbody>
  <tr>
   <td><p><strong>永続性タイプ</strong></p> </td>
   <td><p><strong>データストア</strong></p> </td>
   <td><p><strong>場所</strong></p> </td>
  </tr>
  <tr>
   <td><p>デフォルト</p> </td>
   <td><p>リバースレプリケーション設定で指定されたパブリッシュインスタンスとオーサーインスタンスのAEMリポジトリ</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code><br /> </p> </td>
  </tr>
  <tr>
   <td><p>リモート</p> </td>
   <td><p>リモート処理オーサーインスタンスのAEMリポジトリ</p> </td>
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
| `processedXDP` | 送信済みのレターの作成に使用される XDP テンプレートの詳細が含まれます。 このノードは、送信された通信に対してのみ作成されます。 |
| `submittedLetter` | 送信済みレターデータをダウンロード可能なバイナリ形式で格納します。このノードは、送信された通信に対してのみ作成されます。 |

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

設定済みのデータストア内のドラフトと送信済みの通信データにアクセスし、必要に応じて削除できます。

### ユーザーデータへのアクセス {#access-user-data}

Correspondence Management には、ドラフトインスタンスと送信済みレターインスタンスを検索してアクセスするための API が用意されています。 API を使用すると、レターインスタンス ID または通信を保存または送信したユーザーを使用して、レターインスタンスを検索し、開くことができます。 詳しくは、[レターインスタンスにアクセスするための API](/help/forms/using/cm-apis-to-access-letter-instances.md) を参照してください。

または、CRX DelIte を使用してAEMリポジトリ内のレターインスタンスに移動することもできます。 詳しくは、 [ユーザーデータとデータストア](/help/forms/using/correspondence-management-handling-user-data.md#data) を参照してください。

### ユーザーデータの削除 {#delete-user-data}

特定のユーザーのデータを含むレターインスタンスを検索するには、次の操作を実行します。

* レターインスタンス名、またはドラフトを保存したユーザー、または通信を送信したユーザーが既知の場合は、Correspondence Management API を使用します
* メール ID や名前など、個人を特定できる情報を使用して AEM リポジトリを検索し、情報が格納されているノードを探します

AEM システムでドラフトおよび送信済み通信に含まれるユーザーデータを完全に削除するには、適用可能なすべての AEM インスタンスからレターインスタンスノードを手動で削除する必要があります。
