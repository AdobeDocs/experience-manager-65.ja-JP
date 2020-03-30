---
title: アセットのプレビュー
description: ダイナミックメディアでプレビューアセットを作成する方法を説明します。
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
translation-type: tm+mt
source-git-commit: 43bf1416d9a35b979431466cc83b9baec66ae848

---


# ソフトウェアインターフェイスを使用したアセットのプレビュー {#previewing-assets}

プレビューを使用すると、アップロードしたデジタルアセットが顧客のWebブラウザーでどのように表示されるかを確認できます。 アセットに割り当てられたデフォルトのクロスデバイス対応組み込みビューアがプレビューに使用されます。

ビューアは、コンピューター画面やモバイルデバイスでのリッチメディアアセットの表示方法を決定する、様々な設定（「プリセット」と呼ばれます）のコレクションです。この設定には、ビューアのディスプレイサイズ、ズーム時の動作、配色、境界線、フォントなどが含まれます。

ビデオ、スピンセットおよび画像セット用の専用プレビュー機能を使用できるほか、自分で作成したビューアプリセットを使用してアセットをプレビューすることもできます。または、画像プリセットを使用して画像のレンディションをプレビューします。

* [画像プリセットの適用](/help/assets/image-presets.md)
* [ビューアプリセットの適用](/help/assets/viewer-presets.md)

>[!NOTE]
>
>AEM の Web ページ（Sites）で操作しているときは、**編集**&#x200B;モードでアセットをプレビューできません。**プレビュー**&#x200B;モードに移るには、右上隅の「**プレビュー**」をクリックする必要があります。

To enable or disable viewer presets in the user interface, see [Managing Viewer Presets](/help/assets/managing-viewer-presets.md).

**ユーザインターフェイスを使用してプレビューアセットを作成するには**

1. **[!UICONTROL Adobe Experience Manager**&#x200B;で、**[!UICONTROL ナビゲーション**&#x200B;ページの「**[!UICONTROL アセット]**」をタップし、「**[!UICONTROL ファイル]**」をタップしてアセットにアクセスします。
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL List View]**.
1. （オプション）「**[!UICONTROL 種類]**」列を使用して、プレビューする種類でアセットを並べ替えます。
1. 「**[!UICONTROL タイトル]**」列で、プレビューするアセットの（サムネール画像ではなく）タイトル名をクリックします。
1. クリックしたアセットの種類に応じて、次のいずれかの操作をおこないます。

   <table>
    <tbody>
      <tr>
      <td><strong>クリックしたアセットタイプ</strong><br /> </td>
      <td><strong>特定のレンディションでアセットをプレビューできるか</strong></td>
      <td><strong>特定のビューアでアセットをプレビューできるか</strong></td>
      </tr>
      <tr>
      <td><p>画像</p> </td>
      <td>可</td>
      <td>可</td>
      <td><p><strong>特定のレンディションでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンをクリックして、ドロップダウンリストを表示します。リストから「<strong>レンディション</strong>」をクリックし、プレビューする特定のレンディションを選択します。</li>
        </ul> <p><strong>特定のビューアでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンをクリックして、ドロップダウンリストを表示します。リストから「<strong>ビューア</strong>」をクリックして、アセットに適用するビューアを選択します。</li>
        </ul> <p>Use the <strong>+</strong> and <strong>–</strong> icons to increase or decrease the zoom of the selected image, respectively. Click <strong>Reset</strong> to return the image to the original zoom.<br />モバイルデバイスを使用している場合は、画像をダブルタップして、画像を少しずつズームインできます。最大ズームに達してから、画像を再度ダブルタップすると、ズーム状態がリセットされます。画像全体をドラッグするように動かすと、パンします。</p> </td>
      </tr>
      <tr>
      <td>マルチメディア</td>
      <td>可</td>
      <td>可</td>
      <td><p><strong>特定のレンディションでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンをクリックして、ドロップダウンリストを表示します。リストから「<strong>レンディション</strong>」をクリックし、プレビューする特定のレンディションを選択します。</li>
        </ul> <p>高解像度のビデオレンディションをプレビューすると、ビデオが切り捨てられて表示される場合があります。 これは、レンディションプレビューに、プレビューに使用される埋め込みビューアのコンテキストで、顧客が表示する正確な解像度が表示されるからです。</p> <p>アダプティブビデオセットをプレビューする際、レンディションは1つの再生エクスペリエンスにグループ化されます。 That is, the adaptive video is sized properly for viewing and played back using the best resolution in the context of your viewing device and connection speed.<br /> </p> <p><strong>特定のビューアでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンをクリックして、ドロップダウンリストを表示します。リストから「<strong>ビューア</strong>」をクリックして、アセットに適用するビューアを選択します。</li>
        </ul> </td>
      </tr>
      <tr>
      <td>画像セット</td>
      <td>非対応</td>
      <td>対応</td>
      <td><p><strong>特定のビューアでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンをクリックして、ドロップダウンリストを表示します。リストから「<strong>ビューア</strong>」をクリックして、アセットに適用するビューアを選択します。</li>
        </ul> <p>Use the <strong>+</strong> and <strong>–</strong> icons to increase or decrease the zoom of the selected image, respectively. Click <strong>Reset</strong> to return the image to the original zoom.<br />モバイルデバイスを使用している場合は、画像をダブルタップして、画像を少しずつズームインできます。最大ズームに達してから、画像を再度ダブルタップすると、ズーム状態がリセットされます。画像全体をドラッグするように動かすと、パンします。</p> </td>
      </tr>
      <tr>
      <td>スピンセット</td>
      <td>非対応</td>
      <td>対応</td>
      <td><p><strong>特定のビューアでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンをクリックして、ドロップダウンリストを表示します。リストから「<strong>ビューア</strong>」をクリックして、アセットに適用するビューアを選択します。</li>
        </ul> <p>Use the <strong>+</strong> and <strong>–</strong> icons to increase or decrease the zoom of the selected image, respectively. Click <strong>Reset</strong> to return the image to the original zoom.<br />モバイルデバイスを使用している場合は、画像をダブルタップして、画像を少しずつズームインできます。最大ズームに達してから、画像を再度ダブルタップすると、ズーム状態がリセットされます。画像全体をドラッグするように動かすと、パンします。</p> </td>
      </tr>
      <tr>
      <td>混在メディアセット</td>
      <td>非対応</td>
      <td>対応</td>
      <td><p><strong>特定のビューアでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンをクリックして、ドロップダウンリストを表示します。リストから「<strong>ビューア</strong>」をクリックして、アセットに適用するビューアを選択します。</li>
        </ul> <p>Use the <strong>+</strong> and <strong>–</strong> icons to increase or decrease the zoom of the selected image, respectively. Click <strong>Reset</strong> to return the image to the original zoom.<br />モバイルデバイスを使用している場合は、画像をダブルタップして、画像を少しずつズームインできます。最大ズームに達してから、画像を再度ダブルタップすると、ズーム状態がリセットされます。画像全体をドラッグするように動かすと、パンします。</p> </td>
      </tr>
      <tr>
      <td>カルーセルセット</td>
      <td>非対応</td>
      <td>対応</td>
      <td><strong>特定のビューアでアセットをプレビューするには</strong>：
        <ul>
        <li>ページの左上隅近くにあるアイコンをクリックして、ドロップダウンリストを表示します。アセットに適用するビューアを選択します。</li>
        </ul> </td>
      </tr>
      <tr>
      <td>360 ビデオ<br /> </td>
      <td>可</td>
      <td>可</td>
      <td><p><strong>特定のレンディションでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンをタップして、ドロップダウンリストを表示します。「<strong>レンディション</strong>」を選択した後、プレビューするレンディションを選択します。</li>
        </ul> <p><strong>特定のビューアでアセットをプレビューするには：</strong></p>
        <ul>
        <li>ページの左上隅近くにあるアイコンをタップして、ドロップダウンリストを表示します。「<strong>ビューア</strong>」を選択した後、アセットに適用するビューアを選択します。</li>
        </ul> <p>Use the <strong>+</strong> and <strong>–</strong> icons to increase or decrease the zoom of the selected image, respectively. Click <strong>Reset</strong> to return the image to the original zoom.<br />モバイルデバイスを使用している場合は、画像をダブルタップして、画像を少しずつズームインできます。最大ズームに達してから、画像を再度ダブルタップすると、ズーム状態がリセットされます。画像全体をドラッグするように動かすと、パンします。</p> </td>
      </tr>
    </tbody>
    </table>

## キーボードを使用したアセットのプレビュー {#keyboard-navigation-asset-preview}

1. アセットユーザーインターフェイスから、プレビューするアセットが含まれるフォルダに移動します。

1. フォルダ内で、キーボードのキ `<Tab>` ーまたは矢印キーを押して、アセットを選択します。

1. を押して、 `<Enter>` 選択したアセットをプレビューモードで開きます。

1. 次のいずれかの操作をおこないます。
   * ズームインするには、を `<Tab>` 押してフォーカスをズームイン(+)アイコンに移動し、1回以上を押 `<Enter>` して徐々にズームインします。
   * ズームアウトするには、を `<Tab>` 押してフォーカスをズームアウト(-)アイコンに移動し、1回以上を押して `<Enter>` 徐々にズームアウトします。
   * ズームされたアセットの表示を *水平または* 垂直に移動するには、それぞれの矢印キーを押します。
   * +を押し `<Shift>` て、 `<Tab>` 表示をリセットし、フォーカスをアセットに戻します。
