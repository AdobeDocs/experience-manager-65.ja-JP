---
title: OSGi 上の AEM Forms のグループと権限
seo-title: OSGi 上の AEM Forms のグループと権限
description: ユーザーをグループに割り当てることによる OSGi 上の AEM Forms の管理
seo-description: ユーザーをグループに割り当てることによる OSGi 上の AEM Forms の管理
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
role: Admin
exl-id: d802ac53-e3db-45ca-afcb-7e99d0bb7877
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 79%

---

# OSGi 上の AEM Forms のグループと権限{#aem-forms-on-osgi-groups-and-privileges}

AEM では、[グループを作成](/help/sites-administering/user-group-ac-admin.md#group-administration)してそのグループにポリシーと[ユーザー](/help/sites-administering/user-group-ac-admin.md#user-administration)を割り当てることができます。これらのポリシーは、グループに含まれるユーザーの権限を制御します。

[AEM Formsアドオンパッケージ](../../forms/using/installing-configuring-aem-forms-osgi.md)をインストールすると、この記事に記載されているグループ（forms-usersやforms-power-userなど）が自動的に割り当て可能になります。 次の表に、ユーザーが OSGi 上の AEM Forms でグループの割り当てに基づいて実行できるタスクを示します。

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
     <li>アダプティブフォームを作成、プレビュー、パブリッシュ、送信する</li> 
     <li>インタラクティブ通信とドキュメントフラグメントを作成、プレビュー、パブリッシュする</li> 
     <li>AEM インスタンスにアセットをアップロードする</li> 
     <li>テーマを作成する</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>アダプティブフォームを作成、プレビュー、パブリッシュ、送信する</li> 
     <li>インタラクティブ通信とドキュメントフラグメントを作成、プレビュー、パブリッシュする</li> 
     <li>コードエディターを使用してアダプティブフォームのスクリプトを作成する</li> 
     <li>スクリプトを含むアセットをアップロードする</li> 
     <li>テーマを作成する</li> 
     <li>XDP を含むパッケージを読み込む</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>送信されたフォームをレビューする</li> 
     <li>送信されたフォームを承認または拒否する</li> 
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
   <td><p>FDM 作成者</p> </td> 
   <td>
    <ul> 
     <li>フォームデータモデルを作成および変更する</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>エージェント UI を使用して Correspondence Management レターまたはインタラクティブ通信にアクセスする</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>ワークフロー編集者</p> </td> 
   <td>
    <ul> 
     <li>インボックスアプリケーションを作成する</li> 
     <li>ワークフローモデルを作成する</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>ワークフローユーザー</td> 
   <td>
    <ul> 
     <li>AEMインボックスアプリケーション<br /> <strong>を使用します。注意：</strong>AEMインボックスのインタラクティブ通信エージェントUIにアクセスするには、cm-agent-usersとworkflow-usersのグループ割り当てが必要です。</li> 
     <li>ワークフローインスタンスを管理する</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>FD 管理者</td> 
   <td>
    <ul> 
     <li>PDF Generator を設定する</li> 
     <li>監視フォルダーを設定する</li> 
     <li>ワークフローアプリケーションを管理する</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. forms-usersグループ権限を持つユーザーは、アダプティブフォームのスクリプトを作成できません。
1. template-authors グループ権限を持つユーザーは、テンプレートのスクリプトを書くことができません。
