---
title: Acrobat Reader DC Extensions で使用される証明書の種類
description: Acrobat Reader DC Extensions で使用される証明書の種類について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 800bffd5-0cdc-4251-bba4-e350f226f019
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 23%

---

# Acrobat Reader DC Extensions で使用される証明書の種類 {#certificate-types-used-by-acrobat-reader-dc-extensions}

証明書ビューアは、証明書に関する次の情報を提供します。

* 証明書のわかりやすい名前
* 証明書プロファイル
* 有効期間
* Acrobat Reader DC Extensions の使用権限

## 証明書のわかりやすい名前 {#certificate-friendly-name}

Acrobat Reader DC Extensions 証明書の「わかりやすい」名前は、次の例に示すように、証明書のプロパティを説明する文字列です。

ARE 2D Barcode Full Production V6.1 P8 0002054

文字列には次の要素が含まれます。

**証明書の種類：** 証明書によってアクティベートされる AEM Forms モジュール、およびアクティベートのレベル（ARE 2D Barcode Full など）が記述されています。使用可能な証明書の種類の一覧については、証明書プロファイルの表の種類の列を参照してください。

**デプロイメントの種類：** 実稼働などの、証明書の使用目的を示します。値は、Evaluation（評価）または Production（実稼働環境）のどちらかです。証明書の各種類に関連付けられているデプロイメントの種類の一覧については、証明書プロファイルの表のデプロイメントの種類の列を参照してください。

**使用権限のバージョン：** 証明書を使用できる使用権限アルゴリズムのバージョンが記述されています（V6.1 など）。これは、Acrobat または Acrobat Reader DC Extensions のバージョンではありません。

**プロファイルコード：** プロファイルコードは、完全な証明書プロパティの簡単な説明です（P8 など）。ファイルの各種類に関連付けられているプロファイルコードの一覧については、証明書プロファイルの表のプロファイルコードの列を参照してください。

**シリアル番号：** シリアル番号は、アドビによって発行される証明書ごとにアサインされます（0002054 など）。AdobeエンタープライズサポートまたはAdobeエンタープライズアカウント担当者は、このシリアル番号を使用して、特定の製品の注文または OEM 関係に証明書を追跡できます。

## 証明書プロファイル {#certificate-profiles}

次の表に、Acrobat Reader DC Extensions 証明書を分析する際に発生する可能性のある証明書プロファイルの一覧を示します。

<table>
 <thead>
  <tr>
   <th><p>プロファイルコード</p></th>
   <th><p>タイプ</p></th>
   <th><p>有効期間</p></th>
   <th><p>デプロイメントタイプ</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>SAP 本番環境</p></td>
   <td><p>Max</p></td>
   <td><p>実稼動</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>SAP 内部テスト</p></td>
   <td><p>2 年</p></td>
   <td><p>評価とテスト</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Acrobat Reader DC拡張機能、実稼動</p></td>
   <td><p>Max</p></td>
   <td><p>実稼動</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Acrobat Reader DC Extensions、内部Adobe使用</p></td>
   <td><p>2 年</p></td>
   <td><p>実稼動</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Acrobat Reader DC拡張機能、パートナー統合</p></td>
   <td><p>2 年</p></td>
   <td><p>評価とテスト</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Acrobat Reader DC Extensions，評価</p></td>
   <td><p>60 日</p></td>
   <td><p>評価</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Forms、実稼動</p></td>
   <td><p>Max</p></td>
   <td><p>実稼動</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x、実稼動</p></td>
   <td><p>Max</p></td>
   <td><p>実稼動</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms、OEM で使用可能</p></td>
   <td><p>Max</p></td>
   <td><p>実稼動と評価</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms、OEM で使用可能</p></td>
   <td><p>Max</p></td>
   <td><p>実稼動と評価</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>署名のみ、OEM で使用可能</p></td>
   <td><p>Max</p></td>
   <td><p>実稼動と評価</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>オフラインコメントのみ、OEM で使用可能</p></td>
   <td><p>Max</p></td>
   <td><p>実稼動と評価</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>コメントのみ、OEM で使用可能</p></td>
   <td><p>Max</p></td>
   <td><p>実稼動と評価</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>フルアクセス許可、OEM で使用可能</p></td>
   <td><p>Max</p></td>
   <td><p>実稼動と評価</p></td>
  </tr>
 </tbody>
</table>

## 有効期間 {#validity-period}

評価証明書は、製品のサンプルアプリケーションを評価および開発できるように、顧客および開発者に対して発行されます。 これらの証明書の有効期間は 60 ～ 90 日です。 配信は、問題のデータの後、2 ヶ月目の終わりに期限が切れます。

パートナー統合証明書は、Adobeの開発、統合、プロトタイピング、デモをサポートするために、ソフトウェアビジネスパートナーに対して発行されます。 これらの証明書は、発行日から 2 年間有効です。

Adobe内部使用証明書は、Adobe内で、ソフトウェアの開発、統合、プロトタイピング、デモをサポートするために使用されます。 これらの証明書は、発行日から 2 年間有効です。

実稼動証明書は、 Acrobat Reader DC Extensions を購入した顧客に対して発行されます。 これらの証明書は、次に示すように、認証局 (CA) が許可する最大期間有効です。 *最大* 」と入力します。

## Acrobat Reader DC Extensions の使用権限 {#acrobat-reader-dc-extensions-usage-rights}

証明書ビューアでAcrobat Reader DC Extensions 証明書を確認する際に、「詳細」タブで使用権限項目を選択すると、証明書で有効にできるAdobe Reader使用権限の定義済みリストが表示されます（設定されている場合）。 特定のドキュメントに対して有効な使用権限は、証明書によって有効にされた使用権限のサブセットにすることができます。

共同作業を行わない環境でオンラインコメントが必要な場合は、Adobeサポートにお問い合わせください。 Mode プロパティは、デプロイメントの種類と一致し、次のいずれかです。 *実稼動* または *評価*.

許可されるAcrobat Reader DC Extensions の使用権限は、1 つ以上の特定の要素で構成されます。 これらの要素は、様々な組み合わせで使用され、ライセンスされた製品機能の品種を実現します。

<table>
 <thead>
  <tr>
   <th><p>使用権限要素</p></th>
   <th><p>権限が付与されたPDFドキュメントを表示したときにAdobe Readerで有効になる機能</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>フォームフィールドに入力し、ファイルをローカルに保存します。</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>フォームデータを FDF、XFDF、XML、XDP ファイルとして読み込んだり書き出したりします。</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>PDF・フォームで、フィールドおよびフィールド・プロパティを追加、変更または削除します。</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>ブラウザーセッションで実行されていないサーバーに、電子メールまたはオフラインでデータを送信します。</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>同じテンプレートフォーム内で、テンプレートページからPDFを作成します。</p></td>
  </tr>
  <tr>
   <td><p>署名</p></td>
   <td><p>電子署名を行い、PDFドキュメントを保存し、電子署名を消去します。</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>コメントなどのドキュメント注釈を作成および変更します。</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>コメントなどの注釈を別のデータファイルに保存し、ファイルからコメントを読み込みます。</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlaintext</p></td>
   <td><p>デコードするためにライセンスされたサーバーソフトウェアを必要としない、暗号化されていない形式でバーコードされたフォームデータを含むドキュメントを印刷します。</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>オンラインのドキュメントレビューおよびコメントサーバーに対して、コメントなどの注釈をアップロードおよびダウンロードします。</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>接続フォーム内で定義された Web サービスまたはPDFに接続します。</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>埋め込みファイルオブジェクトをPDF・ドキュメントに変更します。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Acrobat Reader DC Extensions の使用権限は、連携して動作する特定の組み合わせでのみ、Adobeからライセンスできます。 これらの機能を個別にライセンスすることはできません。 使用権限の使用可能な組み合わせについて詳しくは、AEM forms のアカウント担当者にお問い合わせください。
