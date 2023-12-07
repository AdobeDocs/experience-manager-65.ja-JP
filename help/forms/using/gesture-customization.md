---
title: ジェスチャーのカスタマイズ
description: AEM Formsアプリでジェスチャーをカスタマイズする方法を説明します。 ジェスチャーをカスタマイズして、アプリケーションとの個別の対話方法を提供できます。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 68%

---

# ジェスチャーのカスタマイズ {#gesture-customization}

AEM Forms アプリケーションのジェスチャーをカスタマイズして、アプリケーションを操作するための独自の方法を提供できます。例えば、タスクまたはスタートポイントを開いたり閉じたりするジェスチャーを新たに追加できます。

## AEM Formsアプリでジェスチャーをカスタマイズするには {#to-customize-gestures-in-aem-forms-app}

AEM Formsアプリでは、左スワイプは新しいタスクまたは Startpoint を開き、右スワイプは何もしません。 次の例では、AEM Forms アプリケーションで右スワイプジェスチャーを実行したときに新しいタスクまたはスタートポイントを開くための手順を示しています。

1. プロジェクトを開きます。

   * iOS の場合、Xcode で `Capture.xcodeproj` を開きます。
   * Android の場合、Eclipse で Android プロジェクトを開きます。
   * Windows の場合、Visual Studio で `MWSWindows.sln` を開きます。

1. views フォルダーに移動し、`task.js` ファイルを編集用に開きます。

   * Xcode では、**Capture／www／wsmobile／js／runtime／views** フォルダーに移動します。
   * Eclipse では、**assets／www／wsmobile／js／runtime／views** フォルダーに移動します。
   * Visual Studio では、**MWSWindows／www／wsmobile／js／runtime／views** フォルダーに移動します。

   >[!NOTE]
   >
   >task.js ファイルには、タスクリストまたは Startpoint リストに表示されている各タスクまたは Startpoint に関連付けられた Backbone ビューが含まれています。

1. `task.js` ファイルで、ビューのイベントプロパティを検索します。

   イベントプロパティは、各エントリが次の形式で指定されたマップです。

   `"EventName Selector": "Function"`

   トリガー時に、 `EventName`次で指定されたHTML要素に対して： `Selector`、 `Function`が呼び出されます。

1. 検索

   * &quot;select .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;select .last_empty_div&quot; : &quot;onTaskClick&quot;,

   これを

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;、

     &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;、

     &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;、

     &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;、

1. `task.js` ファイルを保存して閉じます。
1. AEM Formsアプリをビルドして実行します。 これで、左スワイプと右スワイプを使用してを開くことができます。

同様に、さまざまな組み合わせのジェスチャー、HTML 要素、および関数に対して、他のビューで変更を行うことができます。
