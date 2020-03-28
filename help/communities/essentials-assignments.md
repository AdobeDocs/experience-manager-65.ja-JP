---
title: 割り当ての基本事項
seo-title: 割り当ての基本事項
description: イネーブルメントコミュニティの割り当て機能の概要
seo-description: イネーブルメントコミュニティの割り当て機能の概要
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# 割り当ての基本事項 {#assignments-essentials}

イネーブルメントコミュニティサイトの割り当て機能を使用するための重要な情報につ [いて説明し](/help/communities/overview.md#enablement-community) ます。

割り当て機能を使用すると、イネーブルメントコミュニティのメンバーに実施可能リソースおよびイネーブルメント学習パスを割り当てることができます。

## クライアント側の基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/myassigned</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.myassigned<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/myassigned.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/clientlibs/myassigned.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>See, <a href="/help/communities/assignments.md">Assignments Feature</a></td>
  </tr>
 </tbody>
</table>

### 完了ステータスと成功ステータス {#completion-and-success-status}

完了ステータスと成功ステータスは、割り当てのレポートおよびステータスバナーで使用されます。

完了ステータス：

* 割り当てなし
* 開始されていません（新規）
* 処理中
* 完了

成功ステータス：

* 不明
* パス
* 失敗

完了ステータスと成功ステータスの組み合わせとして有効なものは以下に限られます。

| **完了** | **成功** |
|---|---|
| 開始されていません | 不明 |
| 処理中 | 不明 |
| 完了 | パス |
| 完了 | 失敗 |

## サーバー側の基本事項 {#essentials-for-server-side}

### 割り当て機能 {#assignments-function}

A community site structure that includes the [Assignments function](/help/communities/functions.md#assignments-function), includes a configured ` [assignments](/help/communities/assignments.md)` component.

### リファレンス API {#reference-apis}

* [イネーブルメント API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [レポート API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [レポート分析 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/analytics/api/package-summary.html)

