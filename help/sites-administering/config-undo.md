---
title: ページ編集のための取り消しの設定
description: AEMでページ編集の取り消しサポートを設定する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 2cf3ac3f-ee17-480d-a32a-c57631502693
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 65%

---

# ページ編集のための取り消しの設定{#configuring-undo-for-page-editing}

[OSGi サービス](/help/sites-deploying/configuring-osgi.md)の **Day CQ WCM Undo Configuration**（`com.day.cq.wcm.undo.UndoConfigService`）では、ページ編集の取り消しおよびやり直しのコマンドの動作を制御するプロパティを確認できます。

## デフォルトの設定 {#default-configuration}

標準インストールでは、デフォルト設定は次の `sling:OsgiConfig` ノード上のプロパティとして定義されています。

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

このノードには、`cq.wcm.undo.whitelist` プロパティと `cq.wcm.undo.blacklist` プロパティが含まれ、その他のプロパティではデフォルトが取得されます。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。

## 取り消しとやり直しの設定 {#configuring-undo-and-redo}

これらの OSGi サービスプロパティは、独自のインスタンス用に設定できます。

>[!NOTE]
>
>AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

次のリストに、Web コンソールに表示されるプロパティと、対応する OSGi パラメーターの名前を、（必要に応じて）説明およびデフォルト値と共に示します。

* **有効にする**
( `cq.wcm.undo.enabled`)

   * **説明**：ページの作成者が変更内容を取り消しおよびやり直しできるかどうかを決定します。
   * **デフォルト**：`Selected`
   * **タイプ**：`Boolean`

* **パス**
( `cq.wcm.undo.path`)

   * **説明**：バイナリの取り消しデータを永続化するリポジトリパス。 作成者が画像などのバイナリデータを変更した場合、元のバージョンのデータはここに保持されます。 バイナリデータへの変更が取り消されると、この取り消しのバイナリデータがページに復元されます。
   * **デフォルト**：`/var/undo`
   * **タイプ**：`String`

  >[!NOTE]
  >
  >デフォルトでは、`/var/undo` ノードにアクセスできるのは管理者のみです。作成者は、バイナリの取り消しデータにアクセスする権限が与えられた後でのみ、バイナリコンテンツに対して取り消しおよびやり直し操作を実行できます。

* **Min.validity**
( `cq.wcm.undo.validity`)

   * **説明**：取り消しのバイナリデータの最短保存時間（時間単位）。この期間を過ぎると、ディスク容量を節約するために、バイナリデータは削除可能になります。
   * **デフォルト**：`10`
   * **タイプ**：`Integer`

* **手順**
( `cq.wcm.undo.steps`)

   * **説明**：取り消し履歴に保存されるページアクションの最大数。
   * **デフォルト**：`20`
   * **タイプ**：`Integer`

* **永続性**
( `cq.wcm.undo.persistence`)

   * **説明**：取り消し履歴を保持するクラス。2 つの永続クラスが用意されています。

      * `CQ.undo.persistence.WindowNamePersistence`：window.name プロパティを使用して履歴を保持します。
      * `CQ.undo.persistence.CookiePersistance`：cookie を使用して履歴を保持します。

   * **デフォルト**：`CQ.undo.persistence.WindowNamePersistence`
   * **タイプ**：`String`

* **永続モード**
( `cq.wcm.undo.persistence.mode`)

   * **説明**：取り消し履歴が保持されるタイミングを決定します。このオプションを選択すると、各ページの編集後に取り消し履歴が保持されます。 ページの再読み込みが発生した場合（例えば、ユーザーが別のページに移動した場合）にのみ保持するには、このオプションをオフにします。

     取り消し履歴の保持には、web ブラウザーのリソースを使用します。ページの編集に対してユーザーのブラウザーの反応が遅い場合は、ページの再読み込み時に取り消し履歴を保持するようにしてください。

   * **デフォルト**：`Selected`
   * **タイプ**：`Boolean`

* **マーカーモード**
( `cq.wcm.undo.markermode`)

   * **説明**：取り消しややり直しが発生したときに影響を受ける段落を示すために使用する視覚的なキューを指定します。次の値を指定できます。

      * flash：段落の選択インジケーターが一時的に点滅します。
      * select：段落が選択されます。

   * **デフォルト**：`flash`
   * **タイプ**：`String`

* **優れたコンポーネント**
( `cq.wcm.undo.whitelist`)

   * **説明**：取り消しコマンドとやり直しコマンドの影響を受けるコンポーネントのリストです。 取り消し/やり直しで正しく機能する場合は、コンポーネントのパスをこのリストに追加します。 コンポーネントをグループで指定するには、アスタリスク（&amp;ast;）を付けます。

      * 次の値は、基盤テキストコンポーネントを指定します。

        `foundation/components/text`

      * 次の値は、すべての基盤コンポーネントを指定します。

        `foundation/components/*`

   * このリストにないコンポーネントに対して取り消しまたはやり直しを実行すると、コマンドの信頼性が低い可能性があることを示すメッセージが表示されます。

   * **デフォルト**：このプロパティには、AEM で提供されている多くのコンポーネントが指定されます。
   * **タイプ**：`String[]`

* **無効なコンポーネント**
( `cq.wcm.undo.blacklist`)

   * **説明**：取り消しコマンドの影響を受けたくないコンポーネントやコンポーネント操作のリスト。取り消しコマンドで正しく動作しないコンポーネントやコンポーネント操作を追加します。

      * 取り消し履歴にコンポーネントの操作を一切必要としない場合（例： ）に、コンポーネントのパスを追加します。 `collab/forum/components/post`
      * 特定の操作を取り消し履歴から除外する場合に、パスにコロン (:) と操作を追加します（他の操作は正しく機能します）。例： `collab/forum/components/post:insertParagraph.`

  >[!NOTE]
  >
  >このリストにある操作は、取り消し履歴に追加されます。 ユーザーは、 **無効なコンポーネント** 操作を元に戻す履歴に含めます。

   * 一般的な操作名は次のとおりです。

      * `insertParagraph`：コンポーネントがページに追加されます。
      * `removeParagraph`：コンポーネントが削除されます。
      * `moveParagraph`：段落が別の場所に移動されます。
      * `updateParagraph`：段落のプロパティが変更されます。

   * **デフォルト**：このプロパティには、複数のコンポーネントの操作が指定されます。
   * **タイプ**：`String[]`
