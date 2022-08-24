---
title: ジェスチャーのカスタマイズ
seo-title: Gesture customization
description: AEM Forms アプリケーションでジェスチャーをカスタマイズ
seo-description: Customize the gestures on your AEM Forms app
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 100%

---

# ジェスチャーのカスタマイズ {#gesture-customization}

AEM Forms アプリケーションのジェスチャーをカスタマイズして、アプリケーションを操作するための独自の方法を提供できます。例えば、タスクまたはスタートポイントを開いたり閉じたりするジェスチャーを新たに追加できます。

## AEM Forms アプリケーションのジェスチャーをカスタマイズするには {#to-customize-gestures-in-aem-forms-app}

AEM Forms アプリケーションで、左スワイプは新しいタスクまたは Startpoint を開き、右スワイプは何もしません。次の例では、AEM Forms アプリケーションで右スワイプジェスチャーを実行したときに新しいタスクまたはスタートポイントを開くための手順を示しています。

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

   `Selector` で指定された HTML 要素で `EventName` という名前の Javascript イベントをトリガーすると、`Function` が呼び出されます。

1. 検索

   * &quot;tap .taskContentArea&quot; : &quot;onTaskClick&quot;、

      &quot;tap .taskOpenArea&quot; : &quot;onTaskClick&quot;、

      &quot;tap .task-content&quot; : &quot;onTaskClick&quot;、

      &quot;tap .last_empty_div&quot; : &quot;onTaskClick&quot;、
   これを

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;、

      &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;、

      &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;、

      &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;、


1. `task.js` ファイルを保存して閉じます。
1. AEM Forms アプリケーションをビルドし実行します。これで、左スワイプと右スワイプを使用してタスクを開くことができます。

同様に、さまざまな組み合わせのジェスチャー、HTML 要素、および関数に対して、他のビューで変更を行うことができます。
