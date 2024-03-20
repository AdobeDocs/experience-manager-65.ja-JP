---
title: ジェスチャーのカスタマイズ
description: AEM Forms アプリのジェスチャーのカスタマイズ方法について説明します。ジェスチャーをカスタマイズして、アプリケーションを操作するための独自の方法を提供できます。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 100%

---

# ジェスチャーのカスタマイズ {#gesture-customization}

AEM Forms アプリケーションのジェスチャーをカスタマイズして、アプリケーションを操作するための独自の方法を提供できます。例えば、タスクまたはスタートポイントを開いたり閉じたりするジェスチャーを新たに追加できます。

## AEM Forms アプリケーションのジェスチャーをカスタマイズするには {#to-customize-gestures-in-aem-forms-app}

AEM Forms アプリケーションでは、左スワイプで新しいタスクまたはスタートポイントを開くことができますが、右スワイプでは何も操作できません。次の例では、AEM Forms アプリケーションで右スワイプジェスチャーを実行したときに新しいタスクまたはスタートポイントを開くための手順を示しています。

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

   * &quot;select .taskContentArea&quot; : &quot;onTaskClick&quot;、

     &quot;select .taskOpenArea&quot; : &quot;onTaskClick&quot;、

     &quot;select .task-content&quot; : &quot;onTaskClick&quot;、

     &quot;select .last_empty_div&quot; : &quot;onTaskClick&quot;、

   これを

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;、

     &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;、

     &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;、

     &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;、

1. `task.js` ファイルを保存して閉じます。
1. AEM Forms アプリケーションをビルドして実行します。これで、左スワイプと右スワイプを使用して開くことができます。

同様に、さまざまな組み合わせのジェスチャー、HTML 要素、および関数に対して、他のビューで変更を行うことができます。
