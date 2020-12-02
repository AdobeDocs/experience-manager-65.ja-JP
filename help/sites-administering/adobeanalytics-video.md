---
title: Adobe Analytics のビデオトラッキングの設定
seo-title: Adobe Analytics のビデオトラッキングの設定
description: SiteCatalyst のビデオトラッキングの設定について説明します。
seo-description: SiteCatalyst のビデオトラッキングの設定について説明します。
uuid: 5a862f05-abfa-42a2-ad40-4c1c32f1bd75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: a18ddac1-9e4c-4857-9cb3-4d5eeb8dd9ec
docset: aem65
translation-type: tm+mt
source-git-commit: 90c99e527a40bb663d4f32d8746b46cf34a2319f
workflow-type: tm+mt
source-wordcount: '1765'
ht-degree: 50%

---


# Adobe Analytics のビデオトラッキングの設定{#configuring-video-tracking-for-adobe-analytics}

ビデオイベントの追跡には、いくつかの方式を使用できます。そのうち 2 つは古いバージョンの Adobe Analytics 用のレガシーオプションで、レガシーマイルストーンとレガシー秒と呼ばれます。

>[!NOTE]
>
>次に進む前に、AEM に&#x200B;**再生可能なビデオ**&#x200B;がアップロードされていることを確認してください。
>
>ページ上でビデオを再生できるようにするには、AEM でビデオファイルをトランスコードする方法について、**[こちらのチュートリアル](/help/sites-authoring/default-components-foundation.md#video)**&#x200B;を参照してください。

各方式を使用してビデオトラッキングのフレームワークを設定するには、以下の手順を実行します。

>[!NOTE]
>
>新規実装の場合は、ビデオトラッキングにレガシーオプションを&#x200B;**使用しない**&#x200B;ことを推奨します。代わりに&#x200B;**マイルストーン**&#x200B;方式を使用してください。

## 共通の手順 {#common-steps}

1. サイドキックから&#x200B;**ビデオコンポーネント**&#x200B;をドラッグし、再生可能なビデオをそのコンポーネントの&#x200B;**アセットとして**&#x200B;追加することによって、Web ページを設定します。

1. [Adobe Analyticsの設定とフレームワークを作成します](/help/sites-administering/adobeanalytics.md)。

   * 以降の節の例では、設定には&#x200B;**my-sc-configuration**&#x200B;という名前を、フレームワークには&#x200B;**videofw**&#x200B;を使用します。

1. フレームワークページで、RSIDを選択し、使用方法を「all」に設定します。 ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. サイドキックの「一般」コンポーネントカテゴリから、ビデオコンポーネントをフレームワークにドラッグします。
1. トラッキング方式を選択します。

   * [マイルストーン](/help/sites-administering/adobeanalytics.md)
   * [非レガシーマイルストーン](/help/sites-administering/adobeanalytics.md)
   * [レガシーマイルストーン](/help/sites-administering/adobeanalytics.md)
   * [レガシー秒](/help/sites-administering/adobeanalytics.md)

1. トラッキング方式を選択すると、それに従って CQ 変数のリストが変更されます。コンポーネントをさらに設定し、CQ変数をAdobe Analyticsのプロパティにマッピングする方法については、次の節を参照してください。

## マイルストーン {#milestones}

マイルストーン方式では、ビデオに関する大部分の情報を追跡します。高度なカスタマイズが可能で、設定が容易です。

マイルストーン方式を使用するには、時間ベースの追跡オフセットを指定して、マイルストーンを定義します。ビデオ再生がマイルストーンを渡すと、ページはAdobe Analyticsを呼び出してイベントを追跡します。 定義したマイルストーンごとに、Adobe AnalyticsプロパティにマップできるCQ変数がコンポーネントによって作成されます。 これらの CQ 変数の名前には、次の形式を使用します。

```shell
eventdata.events.milestoneXX
```

XX というサフィックスは、マイルストーンを定義する追跡オフセットです。例えば、4、8、16、20、28秒のトラックオフセットを指定すると、次のCQ変数が生成されます。

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

次の表に、マイルストーン方式用に提供されているデフォルトの CQ 変数を示します。

<table>
 <tbody>
  <tr>
   <th>CQ 変数</th>
   <th>Adobe Analytics特性</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>これにマッピングされる変数は、DAMに設定されている場合、ビデオの<strong>ユーザーにわかりやすい</strong>名前（<strong>タイトル</strong>）を含みます。これが設定されていない場合は、ビデオの<strong>ファイル名</strong>が代わりに送信されます。 ビデオの再生開始時に一度だけ送信されます。</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>このプロパティにマッピングされる変数には、ファイルの名前が格納されます。eventdata.events.a.media.view と一緒にのみ送信されます。 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>このプロパティにマッピングされる変数には、ファイルのサーバー上のパスが格納されます。eventdata.events.a.media.view と一緒にのみ送信されます。 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>セグメントマイルストーンを通過するたびに送信されます。 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>マイルストーンがトリガーされるたびに送信され、特定のセグメントの視聴に費やした秒数も、このイベントと共に送信されます。例： eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>ビデオビューの初期化時に送信されます。</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>ビデオの再生が終了すると送信<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>特定のマイルストーンが渡されると送信され、Xは、<br />でマイルストーンがトリガされる2番目の値を表します </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>すべてのマイルストーンで送信され、は、Adobe Analytics呼び出しでpev3として表示され、通常は「video」<br />として送信されます。 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eventdata.videoName とまったく同じです。 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>表示されているセグメントに関する情報（例：2:O:4-8）を格納します。 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>DAMで編集するビデオを開き、**タイトル**&#x200B;メタデータフィールドを目的の名前に設定することで、ビデオの&lt;a0/>ユーザーにわかりやすい&#x200B;**名前を設定できます。**

1. 「オフセットを追跡」ボックスで、トラッキング方式としてマイルストーンを選択してから、秒単位の追跡オフセットのコンマ区切りリストを入力します。例えば、次の値はビデオの開始から 4、8、16、20 および 28 秒後にマイルストーンを定義します。

   ```xml
   4,8,16,20,24
   ```

   オフセット値は、0 より大きい整数でなければなりません。デフォルト値は `10,25,50,75` です。

1. CQ変数をAdobe Analyticsプロパティにマップするには、ContentFinderからコンポーネント上のCQ変数の横にあるAdobe Analyticsプロパティをドラッグします。

   マッピングの最適化について詳しくは、『[Adobe Analyticsでのビデオの測定](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)ガイド』を参照してください。

1. [追加](/help/sites-administering/adobeanalytics.md) frameworktoページ。
1. **プレビューモード**&#x200B;で設定をテストするには、ビデオを再生してAdobe Analyticsの呼び出しをトリガーします。

以下のAdobe Analyticsトラッキングデータの例は、4,8,16,20, 24のトラックオフセットと、CQ変数に対する次のマッピングを使用したマイルストーントラッキングに適用されます。

<table>
 <tbody>
  <tr>
   <th>CQ 変数</th>
   <th>Adobe Analytics特性</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>prop2</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>prop3 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>prop4</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>event1</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>event2<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>event3</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>event4<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestone4</td>
   <td>event10</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone8</td>
   <td>event11</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone16</td>
   <td>event12</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone20</td>
   <td>event13</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone24</td>
   <td>event14</td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eVar1, prop1 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>eVar2</td>
  </tr>
 </tbody>
</table>

この例では、ビデオコンポーネントはフレームワークページに次のように表示されます。

![video1](assets/video1.png)

>[!NOTE]
>
>Adobe Analyticsに対する呼び出しを確認するには、DigitalPulse DebuggerやFiddlerなどの適切なツールを使用します。

DigitalPulse Debuggerで表示する場合、前述の例を使用したAdobe Analyticsへの呼び出しは次のようになります。

![chlimage_1-128](assets/chlimage_1-128.png)

*これは、次の値を含む、**Adobe Analyticsに対する**最初の呼び出しです。*

* *eventdata.a.media.name に対する prop1 と eVar1*
* *prop2～4、および contentType（video）と segment（1:O:1-4）を格納している eVar2 と eVar3*
* *eventdata.events.a.media.view にマッピングされた event3*

![chlimage_1-129](assets/chlimage_1-129.png)

*これは Adobe Analytics への&#x200B;**3 回目の呼び出**しです。*

* *prop1 と eVar1 には a.media.name が格納されている*
* *セグメントが表示されたことによって event1 が送信された*
* *再生時間 = 4 で event2 が送信された*
* *eventdata.events.milestone8 に到達したことによって event11 送信された*
* *（eventdata.events.a.media.view がトリガーされなかったので）prop2～4 は送信されない*

## 非レガシーマイルストーン {#non-legacy-milestones}

非レガシーマイルストーン方式は、マイルストーン方式によく似ていますが、マイルストーンを計測の長さの割合に基づいて定義する点が異なります。次の点は共通です。

* ビデオ再生がマイルストーンを渡すと、ページはAdobe Analyticsを呼び出してイベントを追跡します。
* Adobe Analyticsプロパティとのマッピング用に定義されたCQ変数](#cqvars)の[静的セットです。
* 定義したマイルストーンごとに、Adobe AnalyticsプロパティにマップできるCQ変数がコンポーネントによって作成されます。

これらの CQ 変数の名前には、次の形式を使用します。

XX というサフィックスは、マイルストーンを定義する計測の長さの割合です。例えば、10、25、50 および 75 という割合を指定すると、以下の CQ 変数が生成されます。

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. 「オフセットを追跡」ボックスで、トラッキング方式として非レガシーマイルストーンを選択してから、計測の長さの割合のコンマ区切りリストを入力します。例えば、次のデフォルト値は計測の長さの 10、25、50 および 75% でマイルストーンを定義します。

   ```xml
   10,25,50,75
   ```

   オフセット値は、0 より大きい整数でなければなりません。

1. CQ変数をAdobe Analyticsプロパティにマップするには、ContentFinderからコンポーネント上のCQ変数の横にあるAdobe Analyticsプロパティをドラッグします。

   マッピングの最適化について詳しくは、『[Adobe Analyticsでのビデオの測定](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)ガイド』を参照してください。

1. [追加](/help/sites-administering/adobeanalytics.md) frameworktoページ。
1. **プレビューモード**&#x200B;で設定をテストするには、ビデオを再生してAdobe Analyticsの呼び出しをトリガーします。

## レガシーマイルストーン {#legacy-milestones}

この方式は、マイルストーン方式によく似ていますが、「追跡オフセット」**&#x200B;フィールドに指定するマイルストーンが、ビデオ内の設定ポイントではなく割合であるという点が異なります。

>[!NOTE]
>
>「追跡オフセット」フィールドには、1～100 の整数を含むコンマ区切りリストのみを指定できます。

1. 追跡オフセットを設定します。

   * 例：10,50,75,100

   また、Adobe Analyticsに送信される情報はカスタマイズが容易で、マッピングに使用できる変数は3つのみです。

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>これにマッピングされる変数は、DAMに設定されている場合、ビデオの<strong>ユーザーにわかりやすい</strong>名前（<strong>タイトル</strong>）を含みます。タイトルが設定されていない場合は、ビデオの<strong>ファイル名</strong>が代わりに送信されます。 ビデオの再生開始時に一度だけ送信されます。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>このプロパティにマッピングされる変数には、ファイルの名前が格納されます。ビデオの再生開始時に一度だけ送信されます。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>このプロパティにマッピングされる変数には、ファイルのサーバー上のパスが格納されます。ビデオの再生開始時に一度だけ送信されます。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>DAMで編集するビデオを開き、**タイトル**&#x200B;メタデータフィールドを目的の名前に設定することで、ビデオの&lt;a0/>ユーザーにわかりやすい&#x200B;**名前を設定できます。**&#x200B;また、終了したら、変更内容を保存する必要があります。

1. これらの変数を prop1～3 にマッピングします。

   呼び出しの&#x200B;**残りの関連情報**&#x200B;は、**pev3**&#x200B;という名前の&#x200B;**1つの**&#x200B;変数に連結されて送信されます。

   **前述の例を使用したAdobe Analyticsへの** 呼び出しの例は、DigitalPulse Debuggerで表示した場合、次のようになります。

   ![lmilestones1](assets/lmilestones1.png)

   *この呼び出しで送信される&#x200B;**pev3**変数には、以下の情報が格納されます。*

   * *名前*  — ビデオファイル(*film.avi*)の名前。

   * *長さ*  — ビデオファイルの長さ（秒単位）(*100*)

   * *プレーヤー名*  — ビデオファイルの再生に使用するビデオプレーヤー(*HTML5ビデオ*)

   * *再生秒数合計*  — ビデオが再生された秒数の合計(*25*)

   * *開始のタイムスタンプ*  — ビデオ再生がいつ開始したかを識別するタイムスタンプ(*1331035567*)

   * *再生セッション*  — 再生セッションの詳細。このフィールドは、ユーザーによるビデオの操作を示します。例えば、ビデオの再生開始場所、ビデオの前進にビデオスライダーを使用したかどうか、ビデオの再生を停止した場所（*L10E24S58L58 — ビデオが1秒で停止された場合）などのデータが含まれます。セクションL10の25、次に秒にスキップ48*)

## レガシー秒 {#legacy-seconds}

「**レガシー秒**」メソッドを使用すると、Adobe Analyticsの呼び出しはN秒ごとにトリガされます。ここで、NはTrackオフセットフィールドで指定されます。

1. トラックのオフセットを任意の秒数に設定します。

   * 例：6
   >[!NOTE]
   >
   >「追跡オフセット」フィールドに指定できるのは、0 より大きい整数だけです。

   Adobe Analyticsに送信される情報はカスタマイズが容易です。 マッピングに使用できる変数は次の 3 つだけです。

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>これにマッピングされる変数は、DAMに設定されている場合、ビデオの<strong>ユーザーにわかりやすい</strong>名前（<strong>タイトル</strong>）を含みます。タイトルが設定されていない場合は、ビデオの<strong>ファイル名</strong>が代わりに送信されます。 ビデオの再生開始時に一度だけ送信されます。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>このプロパティにマッピングされる変数には、ファイルの名前が格納されます。ビデオの再生開始時に一度だけ送信されます。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>このプロパティにマッピングされる変数には、ファイルのサーバー上のパスが格納されます。ビデオの再生開始時に一度だけ送信されます。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>DAMで編集するビデオを開き、**タイトル**&#x200B;メタデータフィールドを目的の名前に設定することで、ビデオの&lt;a0/>ユーザーにわかりやすい&#x200B;**名前を設定できます。**&#x200B;また、終了したら、変更内容を保存する必要があります。

1. これらの変数を prop1、prop2 および prop3 にマッピングします。

   呼び出しの中の&#x200B;**その他の関連情報**&#x200B;は、**pev3** という&#x200B;**ひとつ**&#x200B;の変数に連結されて送信されます。

   DigitalPulse Debuggerで表示する場合、前述の例を使用したAdobe Analyticsへの呼び出しは次のようになります。

   ![lseconds](assets/lseconds.png)

   *この呼び出しは、前述のレガシーマイルストーン呼び出しと同じです。**[こちら](/help/sites-administering/adobeanalytics.md)**の pev3 に関する情報を参照してください。*

**このチュートリアルで使用しているリファレンス：**

[0] [https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)
