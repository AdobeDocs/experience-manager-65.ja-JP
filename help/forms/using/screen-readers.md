---
title: HTML5 フォーム向けのスクリーンリーダー
seo-title: HTML5 フォーム向けのスクリーンリーダー
description: HTML5 フォームでサポートされるスクリーンリーダーを一覧表示します。
seo-description: HTML5 フォームでサポートされるスクリーンリーダーを一覧表示します。
uuid: 035354e2-957f-4eb6-bc16-4ca96ec7ac74
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# HTML5 フォーム向けのスクリーンリーダー {#screen-readers-for-html-forms}

HTML5 フォームコンポーネントは XFA フォームテンプレートを HTML5 形式にレンダリングします。すべての標準の HTML5 をサポートするブラウザーはこれらのフォームをレンダリングできます。PDF と HTML5 フォーム同士で似たようなデータ取得の経験をサポートするために、PDF フォームのレイアウトは HTML5 フォームで保持されます。

HTML5 フォームは標準の HTML 構成を使用して、これらのフォームとともに通常の HTML のアクセシビリティツールを使用できるようにします。フォームがアクセシビリティを備えたフォームに関するベストプラクティスに従ってデザインされた場合、サポートされているスクリーンリーダーのどれとでも機能します。さらに、そのようなフォームはキーボードナビゲーションに対応しています。

## アクセシビリティの標準 {#accessibility-standards}

HTML5 フォームは既知の例外を含むアクセシビリティのリハビリテーション法第 508 条に準拠します。詳しくは、[HTML5 フォームの VPAT](https://www.adobe.com/mena_en/accessibility/compliance/livecycle-mobile-forms-es4-section-508-vpat.html) を参照してください。

## HTML5 フォーム向けに認定されたスクリーンリーダー {#certified-screen-readers-for-html-forms}

* Microsoft Windows の JAWS 14.0
* Mac OS X と iPad の VoiceOver

### JAWS {#jaws}

すべてのデフォルトのキーストロークとショートカットは HTML5 フォームで機能します。For more information on using JAWS, visit [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp).

### VoiceOver {#voiceover}

HTML5 フォームは VoiceOver のすべてのデフォルトのキーストロークとジェスチャーをサポートします。For more information on setting up and using VoiceOver, see [https://www.apple.com/accessibility/voiceover/](https://www.apple.com/accessibility/voiceover/).

## 既知の問題 {#known-issues}

* **（Internal Explorer 9のみ）** HTML5フォームでは、ページはオンデマンドで（動的に）読み込まれます。 オンデマンドのページ読み込みは、スクリーンリーダーの機能で問題が生じます。スクリーンリーダーのフォーカスがページの最後のフィールドにあり、ユーザーがTabキーを押すと、次のページの最初のフィールドにフォーカスを設定する代わりに、フォームの最初のページの最初のフィールドにフォーカスが戻ります。
* **（Internal Explorer 9 のみ）** HTML5 フォームの日付選択のコントロールはキーボードで完全にアクセスできません。日付選択のコントロールで、上向き／下向き矢印キーを複数回押した場合、日付選択のコントロールが閉じて、フォーカスが次／最後のフィールドに移動します。 

* VoiceOver は、iPad safari では日付ウィジェットで矢印キーを検出できません。
