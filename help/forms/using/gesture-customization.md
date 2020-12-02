---
title: ジェスチャーのカスタマイズ
seo-title: ジェスチャーのカスタマイズ
description: AEM Forms アプリケーションでジェスチャーをカスタマイズ
seo-description: AEM Forms アプリケーションでジェスチャーをカスタマイズ
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 37%

---


# ジェスチャーのカスタマイズ {#gesture-customization}

AEM Formsアプリのジェスチャーをカスタマイズして、アプリと対話する独自の方法を提供できます。 例えば、新しいジェスチャーを追加して、タスクーやStartpointを開いたり閉じたりできます。

## AEM Forms アプリケーションのジェスチャーをカスタマイズするには {#to-customize-gestures-in-aem-forms-app}

AEM Forms アプリケーションで、左スワイプは新しいタスクまたは Startpoint を開き、右スワイプは何もしません。次の例は、AEM Formsアプリで右スワイプジェスチャーを実行したときに新しいタスクまたはStartpointを開く手順を提供しています。

1. プロジェクトを開きます。

   * iOSの場合は、Xcodeで`Capture.xcodeproj`を開きます。
   * Android の場合、Eclipse で Android プロジェクトを開きます。
   * Windowsの場合は、Visual Studioで`MWSWindows.sln`を開きます。

1. 表示フォルダーに移動し、`task.js`ファイルを開いて編集します。

   * Xcodeで、**Capture > www > wsmobile > js > runtime > luntime >表示**&#x200B;フォルダーに移動します。
   * Eclipseで、**assets > www > wsmobile > js > runtime > luntime >表示**&#x200B;フォルダーに移動します。
   * Visual Studioで、**MWSWindows > www > wsmobile > js > runtime > luntime > livers**&#x200B;表示ーに移動します。

   >[!NOTE]
   >
   >task.js ファイルには、タスクリストまたは Startpoint リストに表示されている各タスクまたは Startpoint に関連付けられた Backbone ビューが含まれています。

1. `task.js`ファイルで、表示のイベントプロパティを検索します。

   イベントプロパティは、次の形式の各エントリとのマップです。

   `"EventName Selector": "Function"`

   `Selector`で指定されたHTMLイベントで`EventName`という名前のJavaScript要素をトリガーすると、`Function`が呼び出されます。

1. 検索

   * &quot;tap .taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;tap .taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;tap .タスクコンテンツ&quot; :&quot;onTaskClick&quot;,

      &quot;tap .last_empty_div&quot; :&quot;onTaskClick&quot;,
   これを

   * &quot;swipe .taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;スワイプ。タスクコンテンツ&quot;:&quot;onTaskClick&quot;,

      &quot;スワイプ.last_empty_div&quot; :&quot;onTaskClick&quot;,


1. `task.js`ファイルを保存して閉じます。
1. AEM Forms アプリケーションをビルドし実行します。これで、左スワイプと右スワイプを使用してタスクを開くことができます。

同様に、さまざまな組み合わせのジェスチャー、HTML 要素、および関数に対して、他のビューで変更を行うことができます。
