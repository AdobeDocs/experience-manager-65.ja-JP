---
title: Acrobat Reader DC Extensions で使用される証明書の種類
seo-title: Acrobat Reader DC Extensions で使用される証明書の種類
description: Acrobat Reader DC Extensions で使用される証明書の種類について説明します。
seo-description: Acrobat Reader DC Extensions で使用される証明書の種類について説明します。
uuid: 93c02abc-2d5a-44ed-b93c-981afbd0553d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 331b9317-87b5-4a96-a1bc-429675ff90c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 89%

---


# Acrobat Reader DC Extensions で使用される証明書の種類 {#certificate-types-used-by-acrobat-reader-dc-extensions}

証明書ビューアでは、証明書に関する次の情報を参照できます。

* 証明書のわかりやすい名前
* 証明書プロファイル
* 有効期限
* Acrobat Reader DC Extensions の使用権限

## 証明書のわかりやすい名前  {#certificate-friendly-name}

Acrobat Reader DC Extensions 証明書のわかりやすい名前とは、証明書のプロパティが記述されている文字列です。例を以下に示します。

ARE 2D Barcode Full Production V6.1 P8 0002054

この文字列には、次の要素が含まれています。

**証明書の種類：証明書** がアクティブにするAEM formsモジュール、およびARE 2D Barcode Fullなどのアクティベーションレベルを記述します。使用可能な証明書の種類の一覧については、証明書プロファイルの表の種類の列を参照してください。

**デプロイメントの種類：証明書の使用目的を** 示します（「実稼働」など）。値は、Evaluation（評価）または Production（実稼働環境）のどちらかです。証明書の各種類に関連付けられているデプロイメントの種類の一覧については、証明書プロファイルの表のデプロイメントの種類の列を参照してください。

**使用権限バージョン：V6.1など、証明書を使用できる使用権限アルゴリズムのバージョンを** 説明します。このバージョンは、AcrobatまたはAcrobat Reader DCの拡張機能のバージョンを示しません。

**プロファイルコード：** プロファイルコードは、P8など、完全な証明書プロパティの簡単な説明です。ファイルの各種類に関連付けられているプロファイルコードの一覧については、証明書プロファイルの表のプロファイルコードの列を参照してください。

**シリアル番号：0002054** など、Adobeが発行した各証明書にはシリアル番号が割り当てられます。アドビの販売代理店または営業担当者は、このシリアル番号を使用して、特定の製品注文または OEM 関係まで証明書を追跡できます。

## 証明書プロファイル  {#certificate-profiles}

次の表に、Acrobat Reader DC Extensions の証明書を分析する際に検出される可能性のある証明書プロファイルの一覧を示します。

<table>
 <thead>
  <tr>
   <th><p>プロファイルコード</p></th>
   <th><p>型</p></th>
   <th><p>有効期限</p></th>
   <th><p>デプロイメントの種類</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>SAP 実稼働環境</p></td>
   <td><p>最大</p></td>
   <td><p>実稼動</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>SAP 内部テスト</p></td>
   <td><p>2 年</p></td>
   <td><p>評価およびテスト</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Acrobat Reader DC Extensions、実稼働環境</p></td>
   <td><p>最大</p></td>
   <td><p>実稼動</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Acrobat Reader DC Extensions、Adobe 内部使用</p></td>
   <td><p>2 年</p></td>
   <td><p>実稼動</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Acrobat Reader DC Extensions、パートナー統合</p></td>
   <td><p>2 年</p></td>
   <td><p>評価およびテスト</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Acrobat Reader DC Extensions、評価</p></td>
   <td><p>60 日</p></td>
   <td><p>評価</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Forms、実稼働環境</p></td>
   <td><p>最大</p></td>
   <td><p>実稼動</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x、実稼働環境</p></td>
   <td><p>最大</p></td>
   <td><p>実稼動</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms、OEM で使用可能</p></td>
   <td><p>最大</p></td>
   <td><p>実稼働環境および評価</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms、OEM で使用可能</p></td>
   <td><p>最大</p></td>
   <td><p>実稼働環境および評価</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>署名のみ、OEM で使用可能</p></td>
   <td><p>最大</p></td>
   <td><p>実稼働環境および評価</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>オフラインコメントのみ、OEM で使用可能</p></td>
   <td><p>最大</p></td>
   <td><p>実稼働環境および評価</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>コメントのみ、OEM で使用可能</p></td>
   <td><p>最大</p></td>
   <td><p>実稼働環境および評価</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>全権限、OEM で使用可能</p></td>
   <td><p>最大</p></td>
   <td><p>実稼働環境および評価</p></td>
  </tr>
 </tbody>
</table>

## 有効期限  {#validity-period}

評価用証明書は、製品のサンプルアプリケーションを評価および開発できるようにするために、顧客および開発者に対して発行されます。この証明書の有効期間は 60～90 日です。データが発行されてから 2 か月目の月末に期限が切れます。

パートナー統合証明書は、アドビのビジネスパートナーに対して、ソフトウェアの開発、統合、プロトタイピングおよびデモンストレーションをサポートするために発行されます。この証明書は、発行日から 2 年間有効です。

アドビ内部使用証明書は、ソフトウェアの開発、統合、プロトタイピングおよびデモンストレーションをサポートするために、アドビ システムズ社内で使用されます。この証明書は、発行日から 2 年間有効です。

実稼働環境用の証明書は、Acrobat Reader DC Extensions を購入した顧客に対して発行されます。この種の証明書は、認証局（CA）によって許可された最長期間有効です（証明書プロファイルの表では、「*最大値*」と示されています）。

## Acrobat Reader DC Extensions の使用権限  {#acrobat-reader-dc-extensions-usage-rights}

証明書ビューアで Acrobat Reader DC Extensions 証明書を確認するとき、「詳細」タブで使用権限の項目が設定されている場合にこの項目を選択すると、その証明書で有効にできる Adobe Reader 使用権限の一覧が項目別に表示されます。特定のドキュメントに対して有効にされる使用権限は、証明書によって有効になる権限のサブセットの場合があります。

コラボレーションのない環境でオンライン注釈が必要な場合は、アドビサポートにお問い合わせください。Mode プロパティはデプロイメントの種類と一致し、「*実稼働環境*」または「*評価*」になります。

許可される Acrobat Reader DC Extensions 使用権限は、1 つまたは複数の固有の要素で構成されます。これらの要素を異なる組み合わせで使用することにより、ライセンスされている製品の様々な機能を使用できるようになります。

<table>
 <thead>
  <tr>
   <th><p>使用権限の要素</p></th>
   <th><p>Adobe Reader で有効になる機能（使用権限を付与された PDF ドキュメントを表示する場合）</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>フォームフィールドに入力し、ファイルをローカルに保存する。</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>データを FDF、XFDF、XML または XDP ファイルとして読み込んだり書き込んだりする。</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>PDF フォームのフィールドおよびフィールドプロパティを追加したり、変更したり、削除したりする。</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>サーバーがブラウザーセッションで実行されていないときに、電子メールまたはオフラインでデータをサーバーに送信する。</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>同じ PDF フォーム内のテンプレートページからページを作成する。</p></td>
  </tr>
  <tr>
   <td><p>Signing</p></td>
   <td><p>PDF ドキュメントに電子署名して保存したり、電子署名を消去したりする。</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>コメントなどのドキュメント注釈を作成したり変更したりする。</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>コメントなどの注釈を別のデータファイルに保存したり、ファイルからコメントを読み込んだりする。</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlaintext</p></td>
   <td><p>デコードするためにライセンスされたサーバーソフトウェアを必要としない非暗号化形式でバーコード化されたフォームデータを含むドキュメントを印刷する。</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>コメントなどの注釈を、オンラインドキュメントレビューおよびコメントサーバーにアップロードしたり、サーバーからダウンロードしたりする。</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>PDF フォーム内で定義されている Web サービスまたはデータベースに接続する。</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>PDF ドキュメントに関連付けられた埋め込みファイルオブジェクトを変更する。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Acrobat Reader DC Extensions の使用権限は、連携して動作する特定の組み合わせでのみ、アドビ システムズ社からライセンスを受けることができます。これらの機能を個別にライセンスすることはできません。使用権限の可能な組み合わせについては、AEM Forms の営業担当者にお問い合わせください。

