---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: ' [!DNL Adobe Experience Manager]  6.5 のリリース情報、新機能、インストール方法、詳細な変更リストを確認します。'
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 7e225038e925468f6e4dbdcf1d3dce6eceee9292
workflow-type: tm+mt
source-wordcount: '7156'
ht-degree: 22%

---

# [!DNL Adobe Experience Manager] 6.5 の最新のサービスパックのリリースノート {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE!      DO NOT DELETE THIS HIDDEN NOTE!
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## リリースの概要 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.25.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| タイプ | サービスパックのリリース |
| 日付 | 2026年5月21日<!-- UPDATE FOR EACH NEW RELEASE --> |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

Experience Manager 6.5.25.0には、新機能、お客様が要求した主な機能強化、バグ修正が含まれています。 また、2019年4月以降に利用可能な6.5基盤に基づいて構築されたパフォーマンス、安定性、セキュリティの改善も含まれています。

このサービスパックのリリースでは、重大なバグ修正やセキュリティ強化など、Sites、Assets、Foundation全体で275のバックポートが提供されます。 また、このリリースでは、大規模なキーボードナビゲーション、フォーカス管理、ARIA セマンティクス、カラーコントラストの改善、WCAG標準に沿ったタッチターゲットサイズ変更など、Adobe Experience Manager Sitesのオーサリング全体のアクセシビリティが向上しています。

Crosswalkは、このリリースではデフォルトで使用できるので、インストール後に別のパッケージや設定を必要としません。

セキュリティ バックポートは、XSSの脆弱性に対処し、共有アセット メタデータの処理を改善します。

コンテンツフラグメントとGraphQL APIには、信頼性の向上も加わり、埋め込み画像の参照、永続クエリの処理、エディターのローカライズに対応しています。

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- ## Key features and enhancements -->


## Service Pack 25で修正された問題 {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6525}

#### アクセシビリティ {#sites-accessibility-6525}

* サイトリストビューのテーブル行のドラッグ&amp;ドロップ操作が、キーボードナビゲーションで機能するようになりました。 スクリーンリーダーとキーボードユーザーは、アクション中に行を並べ替えてフィードバックを受け取ることができます。 （SITES-24946）

* レイアウトを編集ツールバーで、画面ラベルとタブレットラベルを意味のあるスクリーンリーダー順序で表示できるようになりました。 ユーザーは、関連する定規の測定値のラベルを聞く代わりに、それらを順番に聞きます。 （SITES-25291）
* 注釈モーダルからスウォッチを開いたときに、スウォッチ ポップオーバーモーダルが正しくフォーカスを管理するようになりました。 フォーカスは、選択したスウォッチボタンに直接移動する代わりに、モーダル見出しから開始されます。 （SITES-25275）
* ティーザーモーダルは、キーボードを使用してダイアログボックスを移動するアクセス可能な方法を提供します。 ユーザーは、ページ上でモーダルの位置を変更するためにマウスを使用する必要がなくなりました。 （SITES-25226）
* カードビューは、不要なARIA グリッド動作を削除することで、アクセシビリティを向上させます。 また、スクリーンリーダーでは、視覚的なレイアウトと一致しないグリッドナビゲーション制御を使用せずに、より明確なカード情報を表示できます。 （SITES-24933）
* 「削除」モーダルのツールヒントが、繰り返しホバーアクションの後も一貫して表示されるようになりました。 ユーザーはポインターを離してアイコンに戻り、ツールヒントをもう一度読むことができます。 （SITES-24778）
* 左側のレールは、ユーザーがサイトのホームページから開いた後、予想される順序でフォーカスを受け取るようになりました。 キーボードとスクリーンリーダーのユーザーは、拡張エリアをスキップすることなく、設定ボタンからパネルのコンテンツに移動できます。 （SITES-24754）
* フォーカス管理は、カルーセルモーダルダイアログボックスで一貫して機能するようになりました。 キーボードとスクリーンリーダーのユーザーは、モーダル見出しから開始し、ダイアログボックスを閉じた後に元のコントロールに戻ることができます。 （SITES-24716）
* リンク選択ダイアログボックスは、ユーザーがダイアログボックスを閉じた後に開いたコントロールにフォーカスを返すようになりました。 キーボードとスクリーンリーダーのユーザーは、ダイアログボックスを閉じた後も場所を失うことがなくなりました。 （SITES-24707）
* 作成者がダイアログボックスを開いたり閉じたりしても、画像モーダルが最初のタブまたはメインページのランドマークにフォーカスを移動しなくなりました。 最初にダイアログボックス見出しにフォーカスを移動してから、ダイアログボックスを開いたコントロールに戻ります。 （SITES-24693）
* モーダルダイアログボックスが開いたときに、参照パネルでフォーカスが正しく管理されるようになりました。 キーボードとスクリーンリーダーのユーザーは、ダイアログボックスを閉じるまでダイアログボックス内に留まり、コンテキストを失うことなくナビゲーションを続行します。 （SITES-24683）
* ハイパーリンクパス選択モーダルは、作成者がフィールドを開いたり閉じたりしたときに、間違ったフィールドやコントロールにフォーカスを移動しなくなります。 フォーカスはモーダル見出しから始まり、モーダルを開いたボタンに戻ります。 （SITES-24672）
* 作成者がティーザーモーダルを開いたり閉じたりしても、最初のタブまたはページの先頭にフォーカスが移動しなくなりました。 フォーカスは、想定されるダイアログボックスのフローに従い、不要なスクリーンリーダーのアナウンスを減らします。 （SITES-24522）

* ページエディターのロックボタンで、より正確なスクリーンリーダーのフィードバックが得られるようになりました。 スクリーンリーダーは、使用可能な場合はtitle属性を使用します。これにより、支援テクノロジーを使用する作成者の詳細な通知が減少します。 （SITES-41431）
* キーボードナビゲーションで非表示のコンテンツがスキップされるようになりました。 ユーザーは、目に見えないコンテンツに集中することなく、目に見えるインターフェイス要素を移動できます。 （SITES-41430）
* ユーザーがオーバーレイを閉じた後、キーボードフォーカスがトリガー要素に戻るようになりました。 ページエディターがオーバーレイにフォーカスを送り返すことがなくなり、キーボードユーザーのナビゲーションが向上しました。 （SITES-40819）
* ユーザーがキーボードを使用してツールバー項目を移動する際に、ページエディターツールバーにツールヒントなどのラベルが表示されるようになりました。 アイテム間でフォーカスが移動する際に、各ツールバーアクションを把握できます。 （SITES-40751）
* コンポーネントブラウザーの項目にマウスポインターを置くと、アクティブテキストコンポーネントからフォーカスが削除されなくなりました。 制作者は、テキストを中断することなく編集でき、キーボードのフォーカスは予測可能なままです。 （SITES-35370）
* スクリーンリーダーが「検索モーダル」のソート方向ボタンをより明確に認識するようになりました。 ボタンラベルが同じ方向を繰り返すことがなくなり、トグル動作をより詳細に説明できるようになりました。 （SITES-25534）
* 検索モーダルで、「ファイルまたはフォルダーを変更」リストボックスに、選択したオプションの視覚的なインジケーターが表示されるようになりました。 ユーザーは、フォーカスだけに頼ることなく、現在のパンくずオプションを特定できます。 （SITES-25532）
* 検索モーダルで、「並べ替え順」ラベルのコントラストが上がりました。 このテキストは、アクセシビリティ要件を満たしており、視力の低いユーザーの読みやすさを向上させます。 （SITES-25531）
* デバイス選択ボタンで、レイアウトを編集ツールバーに正しい現在の状態が表示されるようになりました。 スクリーンリーダーのユーザーは、誤解を招くようなトグルステータスを聞くことなく、アクティブデバイスを識別できます。 （SITES-25524）
* キーボードとスクリーンリーダーのナビゲーションで、フォーカスが移動したときに受信トレイ メニューが閉じるようになりました。 フォーカスが他の場所に移動してもメニューが開いたままになる、混乱を避けることができます。 （SITES-25518）
* キーボードとスクリーンリーダーのナビゲーションで、フォーカスを離れた際にヘルプメニューが閉じるようになりました。 メニューを開いたままにして、フォーカスがメニュー外のコンテンツに移動しなくなります。 （SITES-25517）
* コンテンツフラグメントのホームページで、サイドバータブに一貫したアクセス可能なラベルが提供されるようになりました。 ユーザーがタブコントロールを移動すると、NVDAがタブラベルを正しくアナウンスします。 （SITES-25509）
* ページ情報メニューの焦点を合わせたオプションが、最小限のコントラスト要件を満たすようになりました。 コントラストが改善され、視力の低いユーザーがアクティブなメニュー項目を識別しやすくなりました。 （SITES-25321）
* 折りたたまれたデモグラフィックツールバーで、キーボードナビゲーションが非表示のコントロールをスキップするようになりました。 フォーカスは、表示されるインタラクティブ要素に引き続き適用され、レイアウトプレビューのナビゲーション順序が改善されます。 （SITES-25304）
* デバイスを回転ボタンで、レイアウトを編集ツールバーのスクリーンリーダーのフィードバックがより明確になりました。 スクリーンリーダーは、現在の向きとそれを変更するアクションを通知します。 （SITES-25292）
* 「レイアウトを編集」ツールバーに、「デスクトップ」ボタンの選択状態がクリア表示されるようになりました。 「デスクトップ」オプションは、他のデバイスボタンと一致し、アクティブなビューを識別しやすくします。 （SITES-25290）
* レイアウトを編集ツールバーで、支援テクノロジの定規の領域にラベルが付けられるようになりました。 レイアウト編集中にスクリーンリーダーのユーザーにラベルなし測定値が表示されなくなりました。 （SITES-25287）
* 「レイアウトを編集」ツールバーに、チェックを入れていない状態でiPhone 8 Plusのボタンラベルが表示されるようになりました。 ボタンの周囲に十分なスペースが存在する場合に、ラベルが切り捨てられなくなりました。 （SITES-25284）
* 報告された問題では、複数のデバイスコントロールをカバーするように見える、レイアウトを編集ツールバーのフォーカスインジケーターについて説明しました。 フォーカスのアウトラインに隣接するボタンが含まれている場合に、アクティブコントロールのトラックが失われる可能性があるキーボードユーザーに注目しました。 問題は想定通りに機能していた。 （SITES-25283）
* 報告された問題は、各ボタンラベルの前に注釈を発表した注釈モーダルボタンについて説明しています。 注釈、スウォッチ、削除などのアクションのスクリーンリーダー出力が不明確であることに注目しました。 （SITES-25277）
* 注釈ボタンのテキストで、注釈モーダルで十分なコントラストが使用されるようになりました。 このアップデートは、視力が低いユーザーの読みやすさを向上させ、WCAG コントラスト要件をサポートします。 （SITES-25267）
* ユーザーが「新しいコンポーネントを挿入」リストをフィルターすると、スクリーンリーダーにステータスの更新が表示されるようになりました。 モーダルは結果の変更を通知するので、ユーザーは入力中にリストが変更されたことを理解できます。 （SITES-25251）
* ログに記録された問題では、注釈モーダルタイトルの見出しセマンティクスが欠落していることが説明されています。 懸念は、スクリーンリーダーのナビゲーションとモーダル構造を理解する能力に焦点を当てています。 （SITES-25248）
* ページエディターのサイドパネルの見出しレベルが、より明確なコンテンツ階層に従うようになりました。 左側のレール セクションは、支援テクノロジーのメインページの見出しとしては表示されなくなりました。 （SITES-25222）
* Assetsの左側のレールの「編集」ボタンに、より大きなタッチターゲットが追加されました。 移動が必要なユーザーは、ボタンをより簡単に起動し、近くのコントロールを避けることができます。 （SITES-25221）
* Assetsの左側のレールで、「編集」ボタンが新しいブラウザータブを開くタイミングが特定されるようになりました。 利用者は、コンテキストを予期せず失うのではなく、ナビゲーションの変更を予測することができます。 （SITES-25220）
* ユーザーがテキストスペースを増やしたときに、コンポーネントタイトルが正しく表示されるようになりました。 サイドレールは読み取り可能なラベルを保持し、WCAG テキストの間隔の要件をサポートします。 （SITES-25219）
* サイドレールコンポーネントのフィルターフィールドに、適切なアクセス可能な名前が表示されるようになりました。 このアップデートは、スクリーンリーダーのユーザーがプレースホルダーテキストに依存せずにフィールドを識別するのに役立ちます。 （SITES-25212）
* 報告された問題では、注釈モードで非論理的なフォーカスシーケンスが記述されていました。 キーボードユーザーは、モードをアクティブ化した後にShift + Tab キーを使用しない限り、注釈ツールバーを見逃したと報告されています。 （SITES-24996）
* エディターキャンバスは、そのトップバータイトルを見出しとして表示します。 スクリーンリーダーは、正しい構造でタイトルをアナウンスできるため、ナビゲーションとページの理解が向上します。 （SITES-24993）
* アクセシビリティレポートでは、ユーザーがビューを切り替える際に表示される読み込み状態メッセージのコントラストが不十分であることが示されました。 この懸念は、視力または色覚障害の低いユーザーの読みやすさに焦点を当てています。 （SITES-24991）
* アクセシビリティレポートでは、カードリンクに非記述的なテキストが含まれていることに注意しました。 この懸念事項は、スクリーンリーダーのユーザーが追加のコンテキストなしで各リンク先を理解できるようにすることに重点を置いています。 （SITES-24975）
* サイトリストビューに、ライブコピーのテキストがより強いコントラストで表示されるようになりました。 このアップデートは、視力の低いユーザーや明るい画面で作業するユーザーの読みやすさを向上させます。 （SITES-24956）
* ユーザーがエミュレーターメニューを展開した後、キーボードナビゲーションがエミュレーターメニューにフォーカスを移動するようになりました。 この動作により、スクリーンリーダーやキーボードユーザーは、予想される順序でメニューオプションにアクセスできます。 （SITES-24954）
* サイトのリスト表示で、テーブル行のドラッグ&amp;ドロップボタンの表示が改善されました。 コンテンツの作成者は、コンテンツを並べ替える際に、コントロールをより簡単に特定できます。 （SITES-24951）
* カードが同じ宛先を共有する際に、画像リンクと見出しリンクの両方を個別のリンクとして公開することはなくなりました。 このアップデートにより、スクリーンリーダーの冗長性が軽減され、ナビゲーション効率が向上します。 （SITES-24947）
* ヘッダーメニューボタンでは、より正確なアクセシビリティ属性が使用されるようになりました。 スクリーンリーダーは、ダイアログボックスを開くコントロールではなく、拡張可能なコントロールとしてボタンを読み上げます。 （SITES-24742）
* インボックスで、セマンティックリストマークアップを使用して関連リンクをマークするようになりました。 スクリーンリーダーを使用すると、受信トレイのリンクの数とグループ化をより簡単に把握できます。 （SITES-24730）
* ヘッダーボタンのラベルで、詳細なアクセス可能な名前が避けられるようになりました。 スクリーンリーダーのユーザーは、アイコンテキストから重複する役割情報がなくても、より明確な通知を受け取ることができます。 （SITES-24715）
* 「CSV レポート」ボタンで、新しいタブの動作に関するフィードバックがより明確になりました。 ユーザーは、ボタンを選択すると、新しいブラウザータブがアクティブ化される前に開かれることを理解できます。 （SITES-24704）
* モーダルダイアログボックスで、ヘッダーコントロールに対してより正確なアクセシビリティマークアップが使用されるようになりました。 フルスクリーンボタンのヘルプと切り替えは、インタラクティブなコントロールのままであり、スクリーンリーダーには見出しとして表示されなくなります。 （SITES-24696）
* フィルターレールのランドマークで、目的を識別する明確なラベルが使用されるようになりました。 スクリーンリーダーを利用すれば、複数の類似するランドマークがあるページを自信を持って移動することができます。 （SITES-24686）
* 参照Rail メッセージは、十分なテキストコントラストに依存しているユーザーにとってより読みやすくなりました。 報告された問題には、選択と複数選択のメッセージが含まれており、背景に対して明るすぎるように見えました。 （SITES-24666）
* 検索モーダルで、「場所を削除」ボタンと「閉じる」ボタンに大きなタッチターゲットが表示されるようになりました。 この変化は、手の震え、けいれん、または低視力のユーザーが意図したコントロールを活性化するのに役立ちます。 （SITES-24530）
* Adobe Experience Manager ヘッダーリンクが誤ったARIA属性を使用していることが報告されました。 テストでは、リンクが拡張可能なコンテンツを制御することが確認されたため、既存のアクセス可能な状態は引き続き適切です。 （SITES-24528）
* 署名ボタンのフォーカスインジケーターが、コンポーネントリストにカットオフとして表示されなくなりました。 表示されるアウトラインは、キーボードユーザーがエディターでの位置を追跡するのに役立ちます。 （SITES-24503）
* 報告された問題では、コンポーネントパネルの情報ツールチップアイコンの代替テキストが見つからないことが説明されています。 この問題は再現されませんでしたが、レビューでは、情報アイコンは明確なアクセス可能な名前を公開する必要があることを確認しました。 （SITES-24500）
* ページエディターで、同じラベルの複数の地域ランドマークが表示されなくなりました。 各ランドマークには一意のアクセス可能な名前が付けられたため、スクリーンリーダーのユーザーは現在の地域を識別できます。 （SITES-24497）
* 「ファイルまたはフォルダーを変更」コントロールでは、コントロールラベルが状態情報から分離されるようになりました。 スクリーンリーダーを使用しているユーザーは、ヘッダーコントロールを移動する際に、より短く、明確な名前を聞きます。 （SITES-24496）
* コンテンツフラグメント管理テーブルのインタラクティブコントロールで、標準のキーボードナビゲーションがサポートされるようになりました。 キーボードユーザーは、矢印キーによるナビゲーションのみでボタンやリンクを見つける代わりに、ボタンやリンクにタブで移動できます。 （SITES-24285）
* サイト管理UIで、スクリーンリーダー用に装飾的なグローバルアイコンが正しく処理されるようになりました。 アイコンは空の代替テキストを使用するので、ユーザーは意味のあるインターフェイスコンテンツのみを聞きます。 （SITES-3057）

#### 管理者ユーザーインターフェイス{#sites-adminui-6525}

サイトコンソールに、保存された&#x200B;**リストビュー**&#x200B;列の設定が正しく表示されるようになりました。 作成者が設定ダイアログボックスを再度開くと、選択した列はチェックされたままになり、アクティブな列数は正確に保たれます。 （SITES-38576）

#### クラシック UI{#sites-classicui-6525}

クラシック UI テキストコンポーネントダイアログボックスに、生のHTMLではなく、リッチテキストエディター（RTE）コンテンツが書式付きテキストとして表示されるようになりました。 作成者は、Source モードに切り替えたり、マークアップを手動で削除したりすることなく、既存のテキストを編集できます。 （SITES-38709）

#### コンポーネントコンソール{#sites-component-console-6525}

* ユーザーは、コンポーネントコンソールをローカライズまたはマルチバイト文字で検索できるようになりました。 コンソールには、未翻訳の英語文字列の代わりに、ローカライズされた&#x200B;**Remove** ラベルも表示されます。 （SITES-39747）
* コンポーネントプロパティページで、ツール/コンポーネント/コンポーネントプロパティの文字列がローカライズされるようになりました。 ローカライズされたオーサリングインターフェイスに、未翻訳の英語ラベルが表示されなくなりました。 （SITES-39745）

#### [!DNL Content Fragments]{#sites-contentfragments-6525}

ユーザーがフィルターを選択または変更すると、Assets検索が正しく応答するようになりました。 フィルタリングされた結果セットが期待どおりに更新され、Assets コンソールで信頼性の高い検索の絞り込みが復元されます。 （SITES-38686）

#### [!DNL Content Fragments] - 管理者{#sites-admin-6525}

* Assetsのリストビューに、ロックされたコンテンツフラグメントに対するローカライズされた「チェックアウト済み」ツールチップが表示されるようになりました。 この修正により、作成者がワークフロー行をレビューする際のローカライゼーションの一貫性が向上します。 （SITES-42531）

* AEMは、コンテンツフラグメントのダウンロードダイアログボックスでメインラベルをローカライズするようになりました。 この修正により、英語以外のロケールでダウンロードワークフローの一貫性が維持されます。 （SITES-42534）
* 作成者がAssetsからコンテンツフラグメントの公開をスケジュールすると、AEMが`Later` ステータスラベルを翻訳するようになりました。 この修正により、公開済み列はローカライズされたインターフェイス全体で一貫性を保つことができます。 （SITES-42532）
* 作成者が「タイトル」フィールドに無効な文字を入力すると、コンテンツフラグメントの作成にローカライズされた検証メッセージが表示されるようになりました。 ダイアログボックスに、ローカライズされていない「無効な名前が指定された」文字列が表示されなくなりました。 （SITES-19796）
* コンテンツフラグメントを編集ページで、タグとコレクションにローカライズされたラベルが使用されるようになりました。 作成者には、ローカライズされていない英語の文字列ではなく、翻訳されたフィールド名が表示されます。 （SITES-977）

#### [!DNL Content Fragments] - フラグメントエディター{#sites-fragments-editor-6525}

* 作成者がコンテンツをコレクションから削除すると、コンテンツフラグメントエディター内の関連コンテンツに正しいローカライズされた文字列が表示されるようになりました。 ダイアログボックスは、コンテンツ名を未定義に置き換えなくなりました。 （SITES-33675）
* コンテンツフラグメントエディターに、設定されたプレースホルダーのないタブの翻訳済み「一般」ラベルが表示されるようになりました。 ローカライズされたインターフェイスでは、エディター領域に未翻訳の英語文字列が表示されなくなりました。 （SITES-30715）
* コンテンツフラグメントエディターのコンテンツ参照ピッカーに、許可されたアセットタイプのローカライズされたラベルが表示されるようになりました。 ローカライズされたインターフェイスで、サポートされているアセットカテゴリの英語型名が表示されなくなりました。 （SITES-29699）

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6525}

* DAM ファイル名にスペースまたは非ASCII文字が含まれている場合、GraphQL JSON応答に、コンテンツフラグメントリッチテキストフィールドからの埋め込み画像参照が含まれるようになりました。 この修正は、作成者がアセット名を変更することなく、アプリケーションが参照画像をレンダリングするのに役立ちます。 （SITES-42191）
* コンテンツフラグメントのGraphQL応答で、永続クエリをより確実に処理できるようになりました。 更新により、重複するキャッシュヘッダーが修正され、エンコードされた変数の処理が改善され、見つからないコンテンツや失敗したクエリに対してより明確な応答が返されます。 （SITES-40159）
* GraphQLの永続クエリが、不要なERRORおよびWARN メッセージなしでログ内で実行されるようになりました。 AEMでは、エンコードされた変数が正しく処理されるため、正常なクエリでは誤解を招くような`PersistedQueryServlet`個のエントリが作成されなくなります。 （SITES-39354）

* GraphQL エンドポイントを編集ダイアログボックスで、インターフェイス文字列がローカライズされるようになりました。 ローカライズされたインターフェイスで、コンフィギュレーションメッセージから未翻訳のGraphQL スキーマが取得されたことをユーザーに表示できなくなりました。 （SITES-34018）

#### [!DNL Content Fragments] - GraphQL クエリエディター{#sites-graphql-query-editor-6525}

選択したコンフィギュレーションブラウザー名にCJKまたはキリル文字が含まれている場合、GraphQL クエリエディターを開くことができるようになりました。 エディターには、エラーを表示する代わりに、エンドポイントの永続クエリが表示されます。 （SITES-31616）

#### [!DNL Content Fragments] - モデルとモデルエディター{#sites-models-model-editor-6525}

* 選択した値に有効なモデルタイプが必要な場合、コンテンツフラグメントモデルエディターにローカライズされた検証メッセージが表示されるようになりました。 ローカライズされたインターフェイスに未翻訳の英語メッセージが表示されなくなりました。 （SITES-41117）
* コンテンツフラグメントモデルフィルターパネルで、ステータスとタイトル文字列がローカライズされるようになりました。 モデルタイトル、ステータス、ドラフト、有効、無効などの未翻訳ラベルが表示されなくなりました。 （SITES-30863）

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6525} -->

#### ContextHub{#sites-contexthub-6525}

ContextHubがJavaScript エラーなしで読み込まれ、パーソナライゼーションが中断されるようになりました。 ティーザーやその他のパーソナライズされたエクスペリエンスは、影響を受けるページで正しくレンダリングされます。 （SITES-38430）

<!-- #### Core Backend{#sites-core-backend-6525} -->

#### コアコンポーネント{#sites-core-components-6525}

* リクエストが見つからないDAM リソースをターゲットにした場合に、AEMで繰り返しThumbnailServlet エラーが生成されなくなりました。 サーブレットはリダイレクト後に処理を停止し、NullPointerException エントリがエラーログをフラッディングするのを防ぎます。 （SITES-41238）
* 作成者がコンポーネントダイアログボックスを再度開いたときに、オプションのダイアログボックスフィールドが必須としてフラグ付けされなくなりました。 ダイアログボックスでは、実際に入力が必要なフィールドに焦点を当て、検証を維持します。これにより、タブレベルの誤解を招くようなエラーを防ぐことができます。 （SITES-40449）

* AEMには、Sitesと関連するCloud Services コンポーネントを強化する、いくつかのバックレポート済みのセキュリティ修正が含まれています。 これらの修正により、クロスサイトスクリプティングのリスクが軽減され、影響を受けるオーサリングパスをまたいでリクエスト処理が改善されます。 （SITES-38314）
* 画像v3 コンポーネント設定ダイアログボックスで、ページエディターの文字列がローカライズされるようになりました。 ローカライズされたインターフェイスで画像コンポーネントを設定する際に、作成者に未翻訳のラベルが表示されなくなりました。 （SITES-38726）

<!-- #### Campaign integration{#sites-campaign-integration-6525} -->

<!-- #### ContentHub {#sites-contenthub-6525} -->

#### 横断歩道 {#sites-crosswalk-6525}

* Crosswalkでは、インストール後にパッケージと設定を個別に設定する必要がなくなりました。 AEMには、必要なバンドル、コンテンツパッケージ、システムユーザー、サービスユーザーマッピング、機能トグルが、すぐに使用できるパッケージに含まれています。 （SITES-41417）
* Crosswalk ワークフローは、AEM 6.5で必要なcq-wcm-core サポートで動作するようになりました。 作成者は、コアバンドルを個別に更新することなく、テンプレートを作成アクションとユニバーサルエディターを開くアクションを使用できます。 （SITES-37666）

#### エクスペリエンスフラグメント{#sites-experiencefragments-6525}

作成者がエクスペリエンスフラグメントのバリエーションを作成し、最初の40個を超えてスクロールすると、AEMが正しいテンプレートを読み込めるようになりました。 テンプレートピッカーは、ページネーション中に選択したエクスペリエンスフラグメントパスを保持します。 （SITES-41531）

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6525} -->

#### ローンチ{#sites-launches-6525}

* Sites タイムラインで、AEMがローンチを促進する前にバージョンを作成したときに表示されるメッセージがローカライズされるようになりました。 ローカライズされたインターフェイスに未翻訳の英語文字列が表示されなくなりました。 （SITES-39157）
* ローンチリストに、テンプレートまたはライブコピーの継承なしで作成されたローンチの正しい説明が表示されるようになりました。 ユーザーに、誤解を招く「上書き済み」テンプレートラベルが表示されなくなりました。 （SITES-34229）

<!-- #### Link Checker{#sites-link-checker-6525} -->

#### ローカライゼーション{#sites-localization-6525}

* エクスペリエンスフラグメントのテキストコンポーネントプロパティで、ローカライズされたラベルが使用されるようになりました。 書式メニューに、段落、見出し、引用符、または事前書式設定されたテキストの選択に対するローカライズされていない文字列が表示されなくなりました。 （SITES-15091）

* テンプレートのステータスのテキストが、**ツール** > **一般** > **テンプレート**&#x200B;で正しく整列するようになりました。 更新、有効化、公開されたステータスラベルは、1つの横線に表示されます。 （SITES-36797）
* ページを移動ダイアログボックスに、「日付と時刻を選択」ラベルが表示されるようになりました。 フランス語などのローカライズされたインターフェイスでラベルが切り捨てられなくなりました。 （SITES-36795）
* テンプレートエディターのAssets セクションに、翻訳されたタグラベルが表示されるようになりました。 ローカライズされたオーサリングインターフェイスは、テンプレート設定中に一貫したラベルを表示します。 （SITES-33770）
* テンプレートエディターで、ページポリシーの説明が正しくレンダリングされるようになりました。 ユーザーは、「スタイル」タブの切り捨てテキストなしで、完全なデフォルト CSS クラスのガイダンスを読むことができます。 （SITES-29724）
* 作成者がコンポーネントを削除されたテンプレートにドラッグしようとすると、テンプレートエディターにローカライズされたエラーが表示されるようになりました。 メッセージは、「処理中」の未翻訳の文字列として表示されなくなりました。 （SITES-19313）
* ティーザー設定ウィンドウの「ターゲット」ラベルが、ローカライズされたテキストで表示されるようになりました。 「ハイパーリンク」セクションに、英語以外のロケールの英語文字列が表示されなくなりました。 （SITES-18622）
* ページエディターの「ワークフローを開始」ダイアログボックスに、ローカライズされたワークフローアクションラベルが表示されるようになりました。 作成者は、ワークフローオプションに英語の文字列を表示しなくなりました。 オプションには、承認、公開、リクエスト、非公開のアクションがあります。 （SITES-18103）
* セパレーター編集パネルの「親」ドロップダウンメニューに、切り捨てのないローカライズされた文字列が表示されるようになりました。 作成者は、コンポーネントを設定するときに、完全なラベルを確認できます。 （SITES-17480）
* ページエディターのコンテナコンポーネントスタイルメニューに「全幅」と「固定幅」のローカライズされたラベルが表示されるようになりました。 サポートされているロケールを使用する作成者には、これらの文字列が英語で表示されなくなりました。 （SITES-17478）
* 作成者は、テンプレートコンソールのナビゲーションプロパティ領域で完全なツールチップを読み取れるようになりました。 UIはツールチップを整列させ、テンプレート編集中のテキスト切り捨てを防ぎます。 （SITES-15480）
* 作成者は、参照サイドパネルで「テンプレートを使用したFormsとドキュメント」ラベルを読むことができるようになりました。 テンプレートコンソールで、サポートされているロケールの文字列が切断されなくなりました。 （SITES-13167）
* 参照ビューで、更新エラーメッセージにローカライズされたテキストが使用されるようになりました。 AEMで参照リストを更新できない場合、作成者に翻訳されたメッセージが表示されます。 （SITES-13102）
* フォーム検証で、無効な時間値を含むフィールドが識別されるようになりました。 タイムワープモーダルには、影響を受ける時間または分フィールドを修正できるように、より明確なエラーメッセージが表示されます。 （SITES-10980）
* テンプレートコンソールで、画像を選択ダイアログボックスにローカライズされたAssets ラベルが表示されるようになりました。 作成者がテンプレートプロパティからアセットを参照すると、ラベルが正しく表示されます。 （SITES-8113）

#### MSM - ライブコピー{#sites-msm-live-copies-6525}

* ライブコピーの概要で、関係ステータスビューで日付形式がローカライズされるようになりました。 L **ライブコピーSourceの最終変更日**、**ライブコピーの最終変更日**、**最後にロールアウトされたフィールド**&#x200B;には、ユーザーのロケールに一致する日付が表示されます。 （SITES-40756）
* MSMは、プッシュ時に変更するイベントの詳細をログに記録するようになりました。 追加されたイベント情報は、ロールアウトのアクティビティを追跡し、予期しないページ変更のソースを特定するのに役立ちます。 （SITES-38029）

#### ページエディター{#sites-pageeditor-6525}

* 作成者は、大文字またはスペースを含むタグを作成し、最初のページプロパティの保存時に適用できるようになりました。 AEMは、同じ操作の間にタグを作成し、ページメタデータに正しい値を書き込みます。 （SITES-42550）

* 作成者は、名前にアポストロフィを含むコンテンツフラグメントをDAM フォルダーに作成できるようになりました。 AEMは、エンコードされたフォルダーパスを正しく処理し、作成中にNullPointerExceptionをトリガーしなくなります。 （SITES-38653）

* AEMでは、ページエディターで設定されたコンテンツフラグメントコンポーネントのコピー&amp;ペースト操作がサポートされるようになりました。 コンポーネントはコンテンツフラグメント参照を保持するので、作成者は手動でリオーサリングすることなくコンテンツを複製できます。 （SITES-41586）
* ページエディターで、コンポーネントダイアログボックスに最初のフィールドの説明ツールヒントが正しく表示されるようになりました。 長い説明は表示されたままなので、作成者はツールチップの上部にあるテキストを失うことなくフィールドの指示を確認できます。 （SITES-39937）
* 作成者は、HTTP経由でAEMを使用する際に、リッチテキストエディターリンクダイアログボックスを開くことができるようになりました。 この修正により、HTTPSを使用しないオンプレミス環境のリンク編集が復元されます。 （SITES-39467）

<!-- #### Replication{#sites-replication-6525} -->

<!-- #### Rich Text Editor{#sites-rte-6525} -->

#### ユニバーサルエディター {#sites-universal-editor-6525}

* ユニバーサルエディターは、デフォルトでプレビューモードで開かなくなりました。 AEMでは、プレビューの動作を明示的に要求しない限り、ユーザーを実稼動環境のユニバーサルエディター環境に送信します。 （SITES-37193）
* AEMの開発、迅速な開発、およびステージ環境で、ユニバーサルエディターがプレビューモードで開くようになりました。 「開く」コマンドでは、実稼動以外のインスタンスに対して正しいプレビュー動作が使用されます。 （SITES-33839）

### [!DNL Assets] {#assets-6525}

* My Shares クライアントライブラリが、ページマークアップに追加する前に、共有アセットタイトルデータを安全に処理するようになりました。 生成された共有ページは、操作されたアセットメタデータを通じてユーザーをスクリプトインジェクションに公開しなくなります。 （ASSETS-60898）

* Adobe Stockのライセンスは、Assets ユーザーインターフェイスで正しく動作するようになりました。 AEMがストックアセットのプロファイルと使用権限データを読み込んだ後も、「ライセンス」ボタンが無効のままになりません。 （ASSETS-62610）
* アセットの有効期限に関する通知が、有効期限に近い日付を正しく処理するようになりました。 リマインダーメールは、残りの時間が、8日間の有効期限でアセットをスキップするのではなく、設定されたしきい値に達したときに実行されます。 （ASSETS-57857）

* AEM Assetsで、保存済みの検索条件を選択すると、キーボードナビゲーションが復元されるようになりました。 このインターフェイスを使用すると、Assets ビューを更新したり再起動したりすることなく、ドロップダウンから離れることができます。 （ASSETS-52061）

* 管理者表示のダウンロードワークフローで、ZIP ファイル名が正しく保持されるようになりました。 ZIP アセットをダウンロードすると、ダブル .zip拡張子のファイル名が生成されなくなりました。 （ASSETS-62207）
* Assetsの参照ワークフローで、ファイル名のスペースが正しく処理されるようになりました。 選択したファイル名に1つ以上のスペースが含まれている場合、関連アセットの更新が失敗しなくなりました。 （ASSETS-56418）

#### [!DNL Dynamic Media]{#assets-dm-6525}

「字幕とオーディオトラック」ドロップダウンに、Dynamic Mediaでサポートされている言語としてアラビア語が表示されるようになりました。 このアップデートにより、ユーザーはカスタムの回避策なしでアラビア語の字幕トラックを追加できます。 （ASSETS-61771）

### [!DNL Forms]{#forms-6525}

>[!NOTE]
>
>[!DNL Experience Manager] Formsの修正点は、スケジュールされた[!DNL Experience Manager] サービスパックのリリース日から1週間後に、別のアドオンパッケージを通じて配信されます。 この場合、アドオンパッケージは2026年5月28日木曜日（木）にリリース予定です。 さらに、Formsの修正と機能強化のリストがこのセクションに追加されています。



<!-- ALL THE FORMS BUG FIXES LISTED BELOW GO WITH AEM 6.5.25 FORMS MAY 28 2026 RELEASE!! UNHIDE THEM!! -->




<!-- #### Forms Designer {#forms-designer-6525} -->

<!-- 
* The Output API now handles dynamic form content consistently when PDF generation uses client rendering. Generated PDFs retain scripted description text across affected sections instead of leaving some fields blank. (LC-3928858)
* Document of Record generation now handles repeated panel pagination correctly when parent and child panels use the same "Place Top of Next Page" configuration. Authors no longer lose child panel data during the first repeated panel instance in generated output documents. (LC-3923274)
* Long multiline text fields in PDF preview now flow correctly across pages. The generated PDF no longer duplicates page content or drops hidden text during printing. (LC-3924324)
* Fillable PDFs now reset accessibility data when users clear form fields. Screen readers announce the cleared state correctly instead of reading old field values that no longer appear in the form. (LC-3923872)
* The Accessibility Checker now handles Nepali text correctly during PDF validation. Users can check Nepali-language documents without false accessibility errors tied to character encoding. (LC-3922988) 
-->

<!-- #### XMLFM {#forms-xmlfm-6525} -->

<!-- 
* Generated PDFs now include proper tags for supported form fields that use borders in the template. Screen readers can identify numeric fields, date fields, text fields, and checkboxes more reliably. (LC-3923534)
* Document of Record output now applies the correct tag structure to supported fields that include borders in the template. Numeric, date, text, and checkbox fields remain accessible in the generated PDF. (LC-3923265)
-->

<!-- #### XTG {#forms-xtg-6525} -->

<!-- 
* Forms output now merges XML data correctly when generatePDFOutputBatch generates PDFs in batch mode. The batch process no longer creates documents with blank or missing merged fields. (LC-3924192) 
* Document of Record output now includes nested child panels in the first occurrence of a repeatable panel. Forms that use Top of Next Page pagination no longer drop child panel data from the generated output. (LC-3923923)
* Custom bullet characters in XDP templates now map correctly for accessible PDF output. PAC validation no longer reports that text object characters cannot map to Unicode. (LC-3923079) 
-->


### 基盤 {#foundation-6525}

#### Apache Felix {#foundation-apachefelix-6525}

スタートアップは、Felix ベースの認証のためにCredentialsSupport サービスを正しく接続するようになりました。 これにより、AEMの起動時にトークン認証に影響を与える可能性のある依存関係エラーを回避できます。 （GRANITE-63186）

<!-- #### Campaign{#foundation-campaign-6525} -->

<!-- #### Cloud Services{#foundation-cloudservices-6525} -->

<!-- #### Communities {#foundation-communities-6525} -->

<!-- #### Content distribution{#foundation-content-distribution-6525} -->

#### CRX {#foundation-crx-6525}

AEM 6.5のアップグレード後、CRXDE LiteでJSP ファイルの編集が正常に機能するようになりました。 CodeMirror エディターは、「JSP」タブを空白のままにするのではなく、ファイルコンテンツを読み込みます。 （GRANITE-64333）

<!-- #### Granite{#foundation-granite-6525} -->

<!-- #### Integrations{#foundation-integrations-6525} -->

<!-- #### Jetty{#foundation-jetty-6525} -->

#### ローカライゼーション{#foundation-localization-6525}

* セキュリティ/Trust Storeの証明書アップロードダイアログボックスに、ローカライズされたデータ形式ラベルが表示されるようになりました。 ユーザーが証明書を追加すると、ローカライズされていない英語ラベルが表示されなくなりました。 （NPR-43412）

* キーストアを作成ダイアログボックスで、「キャンセル」ボタンが他のダイアログボックスボタンと整列するようになりました。 ボタンのレイアウトは一貫したままであり、調整から外れることはありません。 （NPR-43291）
* **セキュリティ**/A **Adobe IMS設定**&#x200B;のチェックダイアログボックスに、ローカライズされた確認テキストが表示されるようになりました。 チェックメッセージと削除メッセージは、ローカライズされていない英語文字列として表示されなくなりました。 （NPR-43289）
* ローカライズされたUI ラベルが、影響を受けるダイアログボックスと「キーストア」タブに正しく表示されるようになりました。 Aria-label値は翻訳済み文字列を使用し、パスワードラベルは切り捨てずに表示されます。 （NPR-43285）
* 「新規ユーザーを作成」ワークフローに、無効な文字に対するローカライズ検証エラーが表示されるようになりました。 ユーザーは、ローカライズされていないIllegalArgumentException文字列ではなく、明確で翻訳されたメッセージを受け取ります。 （GRANITE-52920）

<!-- #### Oak {#foundation-oak-6525} -->

#### プラットフォーム{#foundation-platform-6525}

* 「タグ参照を表示」ボタンに、選択したタグの参照数が表示されるようになりました。 このアップデートは、ユーザーが追加のナビゲーションなしでタグの使用状況を理解するのに役立ちます。 （CQ-4355509）
* タグ付けの移動ダイアログボックスで、検証メッセージが正しく配置されるようになりました。 ユーザーが空の必須フィールドを含むダイアログボックスを送信する際に、エラーテキストが検索パスアイコンに表示されなくなりました。 （CQ-4353009）

#### セキュリティ{#foundation-security-6525}

AEMは、client-secretを含むキーワードを許可リストに加えるするようになりました。 サポートされている統合でこれらのクライアント秘密名前付けパターンを使用する場合に、設定の作成が失敗しなくなりました。 （GRANITE-66495）

<!-- #### Sling{#foundation-sling-6525} -->

<!-- #### SPA editor {#foundation-spa-editor-6525} -->

#### 翻訳{#foundation-translation-6525}

アップグレード後に翻訳プロジェクトのステータスカウントが正しく更新されるようになりました。 作成者は、以前のサービスパックの動作から得られた古いメタデータに頼ることなく、ドラフト、処理中、および完了値を確認できます。 （NPR-43418）

#### ユーザーインターフェイス{#foundation-ui-6525}

* 手動で入力したサイトコンソール URLが、目的のページまたはフォルダーパスに解決されるようになりました。 更新後もコンテンツ階層は一貫性を維持し、ベース URLにフォールバックしなくなります。 （NPR-43688）
* AEM 6.5 LTS SP1 インスタンスをLTS SP2にアップグレードした後、Adobe CRX Package Manager テストスイートが失敗しなくなりました。 これで、サムネールリストサーブレットのテストが期待どおりに完了しました。 （NPR-43534）

* ブラウザーが更新されるたびに、Sites コンソールのコンテンツツリーが一貫して読み込まれるようになりました。 コンテンツが存在する場合、作成者には空白の左パネルや「項目がありません」メッセージが表示されなくなりました。 （NPR-43442）

<!-- #### WCM{#foundation-wcm-6525} -->

#### ワークフロー{#foundation-workflow-6525}

* ワークフローモデルエディターで、テナント固有のワークフローモデルパスが正しく検証されるようになりました。 テナントレベルの/conf パスの下にワークフローモデルを保存するお客様は、グローバル設定パスに移動しなくても、これらのモデルを編集できます。 （GRANITE-65376）

* ワークフローモデルエディターで、パス検証時にWindows ファイルパスが正規化されるようになりました。 作成者は、モデルの更新をブロックするアクセス エラーを使用せずに、Windows サーバー上でワークフローモデルを編集できます。 （GRANITE-63692）
* タスク作成に、期限のサーバー側検証が含まれるようになりました。 ユーザーは、開始日より前に発生する期日を指定したタスクを作成できません。これにより、受信トレイのタスクデータの一貫性が維持されます。 （CQ-4362253）
* 名前空間作成で、ローカライズされたテキストが正しく処理されるようになりました。 ユーザーは、「タイトル」フィールドにラテン文字以外の文字を入力し、検証エラーなしで名前空間を作成できます。 （CQ-4355587）

## [!DNL Experience Manager] 6.5.25.0 のインストール{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.25.0には[!DNL Experience Manager] 6.5が必要です。 詳しい手順については、[&#x200B; アップグレードドキュメント &#x200B;](/help/sites-deploying/upgrade.md)を参照してください。<!-- UPDATE FOR EACH NEW RELEASE -->
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip)からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに [!DNL Experience Manager] 6.5.25.0 をインストールします。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> アドビでは、[!DNL Experience Manager] 6.5.25.0 パッケージを削除またはアンインストールすることを推奨しません。 したがって、パッケージをインストールする前に、ロールバックする必要がある場合に備えて `crx-repository` のバックアップを作成する必要があります。 <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### [!DNL Experience Manager] 6.5 へのサービスパックのインストール{#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [&#x200B; ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip)からサービスパックをダウンロードします。<!-- UPDATE FOR EACH NEW RELEASE -->

1. パッケージマネージャーを開き、**[!UICONTROL パッケージをアップロード]**&#x200B;を選択して、パッケージをアップロードします。 詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択して、**[!UICONTROL インストール]**&#x200B;を選択します。

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。 [Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログボックスが終了することがあります。 アドビでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。 アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。 この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでも断続的に発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.25.0 のインストール方法は 2 つあります。<!-- UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。 パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。 ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Experience Manager 6.5.25.0 では、Bootstrap のインストールをサポートしていません。<!-- UPDATE FOR EACH NEW RELEASE -->

**インストールの検証**

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (6.5.25.0)` が表示されます。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン 1.22.20 以降です（web コンソールを使用：`/system/console/bundles`）。 <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### [!DNL Experience Manager] Forms へのサービスパックのインストール{#install-aem-forms-add-on-package}

Experience Manager Forms にサービスパックをインストールする手順について詳しくは、[Experience Manager Forms サービスパックのインストール手順](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)を参照してください。

>[!NOTE]
>
>[AEM 6.5 クイックスタート](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)で使用できるアダプティブフォーム機能は、探索と評価のみを目的として設計されています。 アダプティブフォームの機能には適切なライセンスが必要なので、実稼動環境で使用する場合は、AEM Forms の有効なライセンスを取得することが不可欠です。

### Experience Manager コンテンツフラグメント用の GraphQL インデックスパッケージのインストール{#install-aem-graphql-index-add-on-package}

GraphQL を使用しているお客様は、[Experience Manager コンテンツフラグメントと GraphQL インデックスパッケージ 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=ja#package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip) をインストールする必要があります。

これにより、実際に使用する機能に基づいて、必要なインデックス定義を追加できます。

このパッケージをインストールしないと、GraphQL クエリが遅くなったり失敗したりする場合があります。

>[!NOTE]
>
>このパッケージは、インスタンスごとに 1 度だけインストールします。サービスパックごとに再インストールする必要はありません。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.25.0 の UberJar は、[Maven Central リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.25/)で入手できます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven プロジェクトで UberJar を使用するには、[UberJar の使用方法](/help/sites-developing/ht-projects-maven.md)を参照し、プロジェクト POM に次の依存関係を含めます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.25</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar およびその他の関連アーティファクトは、Adobe のパブリック Maven リポジトリー （`repo.adobe.com`） ではなく、Maven Central リポジトリーで入手できます。 メインの UberJar ファイルの名前は、`uber-jar-<version>.jar`に変更されます。 そのため `classifier` が存在せず、`apis` が値として `dependency` タグに使用されます。



## 廃止される機能および削除された機能{#removed-deprecated-features}

AEM 6.5 で廃止または削除されたすべての機能の詳細なリストについては、[廃止および削除された機能](/help/release-notes/deprecated-removed-features.md)を参照してください。

### AEM Assets REST API でのコンテンツフラグメントのサポート {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2 では、コンテンツフラグメントとモデル管理用の最新の OpenAPI が提供されているので、AEM Assets REST API の古いコンテンツフラグメントサポートエンドポイントは非推奨（廃止予定）となりました。

Adobeでは、これらの古いエンドポイントを提供終了のお知らせまで引き続き利用可能とします。 アドビでは、非推奨（廃止予定）のエンドポイントに対する今後の機能強化を予定していません。

### SPA エディター {#spa-editor}

[SPA Editor](/help/sites-developing/spa-overview.md)は、AEM 6.5のリリース 6.5.25以降の新しいプロジェクトでは非推奨（廃止予定）になりました。 SPA エディターは既存のプロジェクトで引き続きサポートされますが、新しいプロジェクトには使用しないでください。

AEM でヘッドレスコンテンツの管理に推奨されるエディターは次のようになりました。

* ビジュアル編集用の[ユニバーサルエディター](/help/sites-developing/universal-editor/introduction.md)。
* フォームベース編集用の[コンテンツフラグメントエディター](/help/sites-developing/universal-editor/introduction.md)。

## 既知の問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* Oakに関連する&#x200B;**&#x200B;**
サービスパック 13以降では、永続キャッシュに影響する次のエラーログが表示され始めています。

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  または

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  この例外を解決するには、次の手順を実行します。

   1. 次の 2 つのフォルダーを `crx-quickstart/repository/` から削除する

      * `cache`
      * `diff-cache`

   1. サービスパックをインストールするか、Experience Manager as a Cloud Serviceを再起動します。
`cache`と`diff-cache`の新しいフォルダーが自動的に作成され、`error.log`で`mvstore`に関連する例外が発生しなくなります。

* コンテンツモデルのカスタム API 名を使用していた可能性のある GraphQL クエリを、代わりにコンテンツモデルのデフォルト名を使用するように更新してください。

* GraphQL クエリでは、`fragments` インデックスの代わりに `damAssetLucene` インデックスを使用する場合があります。 このアクションは結果的に、GraphQL クエリが失敗するか、実行に非常に長い時間がかかる可能性があります。

  問題を修正するには、`damAssetLucene` では、`/indexRules/dam:Asset/properties` に次の 2 つのプロパティを含むように設定する必要があります。

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  インデックス定義を変更した後、インデックス再作成が必要です（`reindex` = `true`）。

  これらの手順を行うと、GraphQL クエリの実行が高速化されます。

* コンテンツフラグメント、サイト、ページのいずれかを移動、削除、または公開しようとすると、コンテンツフラグメントの参照を取得する際に問題が発生します。バックグラウンドクエリが失敗し、機能が機能しません。
正しい操作を行うには、インデックス定義ノード `/oak:index/damAssetLucene`に次のプロパティを追加する必要があります（インデックス再作成は必要ありません）。

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* [!DNL Experience Manager] インスタンスを 6.5.0 ～ 6.5.4 から Java™ 11 の最新サービスパックにアップグレードすると、`error.log` ファイルに `RRD4JReporter` 例外が表示されます。 例外を停止するには、[!DNL Experience Manager] のインスタンスを再起動します。 <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* ユーザーは、[!DNL Assets] の階層内のフォルダーの名前を変更し、ネストされたフォルダーを [!DNL Brand Portal] に公開できます。 ただし、ルートフォルダーが再公開されるまで、[!DNL Brand Portal] でフォルダーのタイトルは更新されません。

* [!DNL Experience Manager] 6.5.x.x のインストール中に、次のエラーや警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して [!DNL Experience Manager] に Adobe Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。 Target では、「エクスペリエンスフラグメント」／ソース「Adobe Experience Manager」タイプではなく、「HTML」／ソース「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：`granite/operations/maintenance` にメンテナンスウィンドウがありません。
   * SUM、MAX、MIN などの集計関数が使用される場合、アダプティブフォームのサーバー側検証が失敗します （CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：`granite/operations/maintenance` にメンテナンスウィンドウがありません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`：登録状況を未登録に変更する処理が完了するのを待機中にタイムアウトになりました。

* AEM 6.5.15 以降、`org.apache.servicemix.bundles.rhino` バンドルで提供される Rhino JavaScript Engine には、新しい巻上げ動作が追加されました。 strict モード（`use strict;`）を使用するスクリプトでは、正しい変数を宣言する必要があります。 そうしないと、実行されず、ランタイムエラーがスローされます。

* 公式アップデートパッケージを通じてタグ付け関連の標準コンテンツをインストールすると、`/content/cq:tags` ノードの言語プロパティがデフォルトにリセットされます。 このアクションは、サービスパック、セキュリティサービスパック、拡張機能パック、累積機能パック、パッチなどに当てはまります。 したがって、インストール前にプロパティから追加しておく必要があります。

### AEM Sites の既知の問題 {#known-issues-aem-sites-6525}

コンテンツフラグメント - 大きなフラグメントツリーに対する DoS 保護が原因でプレビューに失敗します。 詳しくは、[GraphQL Query Executor のデフォルト設定オプションに関するナレッジベース記事](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-23945)（SITES-17934）を参照してください。

### AEM Forms の既知の問題 {#known-issues-aem-forms-6525}

* **FORMS-14521** XML データが保存された下書きレターをプレビューしようとすると、特定のレターに対して`Loading`状態で停止します。
* **FORMS-16603** Interactive Communications Agent UIの印刷プレビューで、一部の計算値が正しく表示されません。
* **FORMS-15681**&#x200B;文字が印刷プレビューで表示されると、内容が変更されます。一部のスペースが消え、特定の文字が`x`に置き換えられます。
* **FORMS-15428** Forms アドオンを使用してAEM Forms Service Pack 20 （6.5.20.0）に更新した後、資格情報ベースの認証を使用する従来のAdobe Analytics Cloud サービスに依存する設定が機能しなくなります。 この問題により、分析ルールが正しく実行されなくなりました。
* **FORMS-16557** Interactive Communications Agent UIの印刷プレビューで、すべてのフィールド値に通貨記号（ドル記号$）が表示される場合があります。 999 までの値の場合は表示されますが、1000 以上の値の場合は表示されません。
* **FORMS-16575** インタラクティブ通信内のネストされたレイアウトフラグメントのXDPに対する変更は、IC エディターに反映されません。
* **FORMS-21378** サーバーサイド検証（SSV）が有効になっている場合、フォーム送信が失敗する可能性があります。 この問題が発生した場合は、アドビサポートにお問い合わせください。
* **FORMS-23722** `bindref`を使用する&#x200B;**添付ファイル** フィールドを含むフォームが、**タスクの割り当て**&#x200B;手順でAEM ワークフローに送信された場合、添付ファイルは表示されません。 その結果、タスクがインボックスから開かれたときに表示されません。 ファイルはリポジトリに正しく保存されますが、タスクを割り当て手順UIで添付ファイルが表示されません。
* アダプティブフォームがSites ページに埋め込まれている場合、**FORMS-23802** カスタム関数をプレビューまたは公開で読み込むことができません。 この問題は、**aem-forms-core-component** ライブラリのバージョンが1.1.76より前の場合に発生します。 ログに`InvalidFormContainerException: No form container found`などのエラーが表示される場合があります。 この問題を解決するには、AEM Forms SP24 （AddOn 6.0.1454）のホットフィックス [&#128279;](/help/release-notes/aem-forms-hotfix.md)を ダウンロードしてインストールします。

#### 利用可能なホットフィックスに関する既知の問題 {#aem-forms-issues-with-hotfixes}

<!--
>[!NOTE]
>
>Avoid upgrading to Service Pack 6.5.25.0 for issues without an available hotfix. It may lead to unexpected errors. Upgrade to Service Pack 6.5.25.0 only after the required hotfixes are released.
-->

次の問題には、ダウンロードとインストールが可能なホットフィックスがあります。 これらの問題を解決するには、[ホットフィックスをダウンロードしてインストール](/help/release-notes/aem-forms-hotfix.md)してください。

* **FORMS-23881** 6.5.23.0 フルインストーラーを使用して設定されたAEM Forms JEE デプロイメントでは、呼び出しでカスタム XCI ファイルが指定されると、Output Serviceでリクエストを処理できません。 この問題を解決するには、[&#x200B; ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html) ポータルから最新のAEM 6.5.25.0 Forms Service Packをインストールしてください。
* **FORMS-23789** （JEE上のAEM Formsのみ）:JEE上のAEM Forms SP24でLog4jに関する問題が発生し、エンタープライズ版のお客様のログ記録とモニタリングに障害が発生しました。 この問題を解決するには、[JEE Service Pack 6.5.25.0でAEM Formsのホットフィックス &#x200B;](/help/release-notes/aem-forms-hotfix.md)をダウンロードしてインストールします。
* **FORMS-23802** フォームが古いaem-forms-core-component バージョン （&lt;1.1.76）のSites ページにある場合、カスタム関数はプレビューまたは公開で読み込まれません。 この問題を解決するには、SP24用の[AEM Forms AddOn ホットフィックス 6.0.1454](/help/release-notes/aem-forms-hotfix.md)をインストールしてください。
* **FORMS-23789** （JEE上のAEM Formsのみ）:JEE上のAEM Forms SP24でLog4jに関する問題が発生し、エンタープライズ版のお客様のログ記録とモニタリングに障害が発生しました。 この問題を解決するには、[JEE Service Pack 6.5.25.0でAEM Formsのホットフィックス &#x200B;](/help/release-notes/aem-forms-hotfix.md)をダウンロードしてインストールします。
* **FORMS-23802** フォームが古いaem-forms-core-component バージョン （&lt;1.1.76）のSites ページにある場合、カスタム関数はプレビューまたは公開で読み込まれません。 この問題を解決するには、SP24用の[AEM Forms AddOn ホットフィックス 6.0.1454](/help/release-notes/aem-forms-hotfix.md)をインストールしてください。
* AEM Forms には、フォームコンポーネントの Struts バージョンが 2.5.33 から 6.x へのアップグレードが含まれるようになりました。 このアップグレードでは、SP24に含まれていなかったStrutsの以前の変更が提供されます。 このサポートは、ダウンロードしてインストールすることで最新バージョンの Struts のサポートを追加できる、[ホットフィックス](/help/release-notes/aem-forms-hotfix.md)を介して追加されました。
* **FORMS-14926** AEM Forms JEE サービスパック 21 （6.5.21.0）をインストールした後、`<AEM_Forms_Installation>/lib/caching/lib` フォルダーの下にGeode jar `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`の重複するエントリが見つかった場合は、次の手順を実行して問題を解決します。

   1. ロケーターが実行中の場合は、ロケーターを停止します。
   2. AEM サーバーを停止します。
   3. `<AEM_Forms_Installation>/lib/caching/lib` に移動します。
   4. `geode-*-1.15.1.2.jar` を除くすべての Geode パッチファイルを削除します。 `version 1.15.1.2` を含む Geode jar のみが存在することを確認します。
   5. 管理者モードでコマンドプロンプトを開きます。
   6. `geode-*-1.15.1.2.jar` ファイルを使用して Geode パッチをインストールします。

* **FORMS-15256** ユーザーがAEM 6.5 Forms サービスパック 18または19からサービスパック 20または21にアップグレードすると、JSP コンパイルエラーが発生しました。 このエラーにより、アダプティブフォームを開いたり、作成したりすることができませんでした。 また、他の AEM インターフェイスでも問題が発生しました。 これらのインターフェイスには、ページエディター、AEM Forms UI、ワークフローエディター、システム概要 UI が含まれていました。

  このような問題が発生した場合は、次の手順を実行して解決します。
   1. CRXDE のディレクトリ `/libs/fd/aemforms/install/` に移動します。
   2. `com.adobe.granite.ui.commons-5.10.26.jar` という名前のバンドルを削除します。
   3. AEM サーバーを再起動します。

* **FORMS-23703** `contains` ルールがデフォルト値なしで設定されていると、アダプティブフォームのサーバーサイド検証が失敗します。 最新バージョンの[AEM Forms 6.5.25.0 サービスパック &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases)をインストールして、問題を修正できます。
* **GRANITE-63681** デフォルトのシステム設定では、必須のキーワードと正規表現パターンがブロックされ、フォームデータモデルコネクタの認証が妨げられます。 この問題を解決するには、[&#x200B; リンク &#x200B;](/help/release-notes/aem-forms-hotfix.md)からホットフィックスをダウンロードしてインストールします。
* **FORMS-23979** HTMLからPDFへのコンバージョン （PDFG）が断続的にタイムアウトする場合があります。 その後、SP24用Forms アドオンの新バージョンがリリースされ、この修正が含まれています。 この問題が発生した場合は、6.5.25.0[&#128279;](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases)の最新リリースのForms アドオンに更新してください。
* **FORMS-23717** **AEM Forms6.5.25.0**&#x200B;にアップグレードした後、`server.log`および`error.log`は、*セキュアパーサーファクトリの作成に失敗*&#x200B;または&#x200B;*セキュリティ属性…がサポートされていません*&#x200B;などの繰り返しのWARN メッセージで溢れることがあります。 ログは、1秒あたり約&#x200B;**5～10行** （1時間あたり数百MB）増加する可能性があります。これにより、ディスクが一杯になり、本番環境のロールアウトがブロックされる可能性があります。

ログ量を減らすには、アプリケーションサーバー設定で`com.adobe.util.XMLSecurityUtil`のログレベルを`ERROR`に設定するか、JVM引数`-Dlogging.level.com.adobe.util.XMLSecurityUtil=ERROR`を使用します。 この機能は、メッセージを非表示にするだけで、根本的な原因を修正しません。

* **FORMS-23875** フォームデータモデル検索では、UIに関連するエンティティが存在しない場合でもHTML タグが表示されます。 この問題を解決するには、[&#x200B; リンク &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bb-expressionmanager-pkg-10.0.48.zip)からホットフィックスをダウンロードしてインストールします。

## 含まれている OSGi バンドルとコンテンツパッケージ{#osgi-bundles-and-content-packages-included}

次のzip ファイルには、この[!DNL Experience Manager] 6.5 Service Pack リリースに含まれているOSGi バンドルとコンテンツパッケージを一覧表示するテキストドキュメントが含まれています。

* [Experience Manager 6.5.25.0](/help/release-notes/assets/65250-bundles.zip)に含まれるOSGi バンドルの一覧
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Managerに含まれるコンテンツパッケージの一覧6.5.25.0](/help/release-notes/assets/65250-packages.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト{#restricted-sites}

これらの Web サイトは、お客様のみが利用できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com での製品のダウンロード。](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-65)
>* [アドビ製品アップデートの優先通知を購読](https://www.adobe.com/subscription/priority-product-update.html)



