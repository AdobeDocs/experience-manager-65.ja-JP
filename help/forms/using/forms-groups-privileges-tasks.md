---
title: OSGi 上の AEM Forms のグループと権限
seo-title: AEM Forms on OSGi Groups and Privileges
description: ユーザーをグループに割り当てて、OSGi 上でAEM Formsを管理する
seo-description: Assign users to the groups to manage AEM Forms on OSGi
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
role: Admin
exl-id: d802ac53-e3db-45ca-afcb-7e99d0bb7877
source-git-commit: 3bc61e56d2fcd9f32c37a7ea04b0ffc6728bfc56
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 53%

---

# OSGi 上の AEM Forms のグループと権限{#aem-forms-on-osgi-groups-and-privileges}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/forms-groups-privileges-tasks.html) |
| AEM 6.5 | この記事 |

以下が可能です。 [グループを作成](/help/sites-administering/user-group-ac-admin.md#group-administration) およびポリシーを割り当てます。 [ユーザー](/help/sites-administering/user-group-ac-admin.md#user-administration) をAEMのグループに追加します。 これらのポリシーは、グループに属するユーザーの権限を制御します。

[AEM Forms アドオンパッケージ](../../forms/using/installing-configuring-aem-forms-osgi.md)をインストールすると、この記事に記載されている forms-user や forms-power-user などのグループは、自動的に割り当て可能になります。次の表に、ユーザーが OSGi 上の AEM Forms でグループの割り当てに基づいて実行できるタスクを示します。

<table>
 <tbody>
  <tr>
   <td>グループ</td> 
   <td>タスク</td> 
  </tr>
  <tr>
   <td>forms-users <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>アダプティブフォームの作成、プレビュー、公開、送信</li> 
     <li>インタラクティブ通信とドキュメントフラグメントを作成、プレビュー、公開する</li> 
     <li>アセットのAEMインスタンスへのアップロード</li> 
     <li>テーマを作成</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>アダプティブフォームの作成、プレビュー、公開、送信</li> 
     <li>インタラクティブ通信とドキュメントフラグメントを作成、プレビュー、公開する</li> 
     <li>コードエディターを使用してアダプティブフォームのスクリプトを作成する</li> 
     <li>スクリプトを含むアセットのアップロード</li> 
     <li>テーマを作成</li> 
     <li>XDP を含むパッケージのインポート</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>送信をレビュー</li> 
     <li>送信を承認または却下</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-authors <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>アダプティブフォームやインタラクティブ通信テンプレートを作成およびプレビューする</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>フォームデータモデルを作成および変更</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>エージェント UI を使用して Correspondence Management レターまたはインタラクティブ通信にアクセス</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> 
     <li>インボックスアプリケーションの作成</li> 
     <li>ワークフローモデルを作成</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>AEM インボックスアプリケーションの使用<br /> <strong>メモ： </strong>AEM インボックスのインタラクティブ通信エージェント UI にアクセスするには、cm-agent-users グループと workflow-users グループに割り当てられている必要があります。</li> 
     <li>ワークフローインスタンスを管理</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administrators</td> 
   <td>
    <ul> 
     <li>PDF Generator を設定</li> 
     <li>監視フォルダーを設定</li> 
     <li>ワークフローアプリケーションを管理する</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. forms-user グループ権限を持つユーザーは、アダプティブフォームのスクリプトを書くことができません。
1. template-authors グループ権限を持つユーザーは、テンプレートのスクリプトを書くことができません。
