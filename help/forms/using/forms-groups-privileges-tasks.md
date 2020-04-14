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
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0

---


# OSGi 上の AEM Forms のグループと権限{#aem-forms-on-osgi-groups-and-privileges}

AEM では、[グループを作成](/help/sites-administering/user-group-ac-admin.md#group-administration)してそのグループにポリシーと[ユーザー](/help/sites-administering/user-group-ac-admin.md#user-administration)を割り当てることができます。これらのポリシーは、グループに含まれるユーザーの権限を制御します。

[AEM Forms アドオンパッケージ](../../forms/using/installing-configuring-aem-forms-osgi.md)をインストールすると、この記事に記載されている forms-user や forms-power-user などのグループは、自動的に割り当て可能になります。次の表に、ユーザーが OSGi 上の AEM Forms でグループの割り当てに基づいて実行できるタスクを示します。

<table>
 <tbody>
  <tr>
   <td>グループ</td> 
   <td>タスク</td> 
  </tr>
  <tr>
   <td>forms-user <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>アダプティブフォームを作成、プレビュー、パブリッシュ、送信する</li> 
     <li>インタラクティブ通信とドキュメントフラグメントを作成、プレビュー、パブリッシュする</li> 
     <li>AEM インスタンスにアセットをアップロードする</li> 
     <li>テーマを作成する</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-user</td> 
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
   <td>template-authors <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>アダプティブフォームやインタラクティブ通信テンプレートを作成およびプレビューする</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-power-user</td> 
   <td>
    <ul> 
     <li>アダプティブフォームやインタラクティブ通信テンプレートを作成およびプレビューする</li> 
     <li>コードエディターを使用して、アダプティブフォームまたはインタラクティブな通信テンプレートのスクリプトを作成する</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
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
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> 
     <li>インボックスアプリケーションを作成する</li> 
     <li>ワークフローモデルを作成する</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>AEMインボックスアプリケーションを使用<br /><strong>する注意：AEMのイン </strong>ボックスでInteractive Communications Agent UIにアクセスするには、cm-agent-usersおよびworkflow-usersグループの割り当てが必要です。</li> 
     <li>ワークフローインスタンスを管理する</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administrators</td> 
   <td>
    <ul> 
     <li>PDF Generator を設定する</li> 
     <li>監視フォルダーを設定する</li> 
     <li>ワークフローアプリケーションを管理する</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. forms-user グループ権限を持つユーザーは、アダプティブフォームのスクリプトを書くことができません。
1. template-authors グループ権限を持つユーザーは、テンプレートのスクリプトを書くことができません。

