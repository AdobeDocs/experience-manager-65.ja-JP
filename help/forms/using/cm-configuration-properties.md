---
title: Correspondence Management設定プロパティ
description: このトピックでは、ソリューション固有の設定で Asset Composer を変更する方法について説明します。 このトピックでは、編集可能なプロパティの説明、デフォルト値、許容可能な値と共に詳細を説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: c9c007d0-c545-4738-b11b-4c50986342ee
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 9%

---

# Correspondence Management設定プロパティ {#correspondence-management-configuration-properties}

これらのプロパティを設定するには、ブラウザーで URL `https://<server>:<port>/<contextPath>/system/console/configMgr` を開き、**Correspondence Management 設定** を選択してください。

Correspondence Management には以下の設定プロパティがあります。

<table>
 <tbody>
  <tr>
   <th><p><strong>プロパティ</strong></p> </th>
   <th><p><strong>説明</strong></p> </th>
   <th><p><strong>デフォルト</strong></p> </th>
   <th><p><strong>指定できる値</strong></p> </th>
  </tr>
  <tr>
   <td><p>インデント</p> </td>
   <td>モジュールのインデント<p> </p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任意の数値</p> </td>
  </tr>
  <tr>
   <td>最小幅の数値</td>
   <td>ローマ数字以外の番号付きリストを使用する場合に、箇条書き/番号フィールドに適用される最小の幅</td>
   <td>8.0mm</td>
   <td>任意の数値</td>
  </tr>
  <tr>
   <td><p>最小幅のローマ数字</p> </td>
   <td><p>ローマ数字を使用する場合に箇条書き/数値フィールドに適用される最小の幅</p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任意の数値</p> </td>
  </tr>
  <tr>
   <td>レンディションタイプ</td>
   <td>通信を作成アプリケーションがレターのプレビューをレンダリングする際に使用するレンディションの種類。 </td>
   <td>HTMLレンディション</td>
   <td>HTMLレンディション/PDFレンディション</td>
  </tr>
  <tr>
   <td><p>CCRPDFハイライトを有効にする</p> </td>
   <td><p>通信を作成アプリケーションのPDFのハイライト表示を有効にします</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>対象のハイライトの種類</p> </td>
   <td><p>通信を作成アプリケーションでの対象のハイライトの種類</p> </td>
   <td><p>境界線</p> </td>
   <td><p>境界線/塗り/なし</p> </td>
  </tr>
  <tr>
   <td><p>対象のハイライトカラー</p> </td>
   <td><p>通信を作成アプリケーションでの対象のハイライトの色</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>任意のRGBカラー（R;G;B 形式）</p> </td>
  </tr>
  <tr>
   <td><p>コンテンツのハイライトの種類</p> </td>
   <td><p>通信を作成アプリケーションでのコンテンツのハイライトの種類</p> </td>
   <td><p>塗り</p> </td>
   <td><p>境界線/塗り/なし</p> </td>
  </tr>
  <tr>
   <td><p>コンテンツのハイライトカラー</p> </td>
   <td><p>通信を作成アプリケーションでのコンテンツのハイライトの色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>任意のRGBカラー（R;G;B 形式）</p> </td>
  </tr>
  <tr>
   <td><p>フィールドのハイライトの種類</p> </td>
   <td><p>通信を作成アプリケーションでのフィールドのハイライトの種類</p> </td>
   <td><p>塗り</p> </td>
   <td><p>境界線/塗り/なし</p> </td>
  </tr>
  <tr>
   <td><p>フィールドのハイライトの色</p> </td>
   <td><p>通信を作成アプリケーションでのフィールドのハイライトの色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>任意のRGBカラー（R;G;B 形式）</p> </td>
  </tr>
  <tr>
   <td><p>アプリケーションタイムアウト</p> </td>
   <td><p>アプリケーションのタイムアウト（秒）</p> </td>
   <td><p>1200</p> </td>
   <td><p>任意の数値</p> </td>
  </tr>
  <tr>
   <td><p>PDFドキュメントのパラメーター名</p> </td>
   <td><p>後処理中のPDFドキュメントのパラメーター名</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>XML データのパラメーター名</p> </td>
   <td><p>後処理での XML ドキュメント（データ）のパラメーター名</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>XDP ドキュメントのパラメーター名</p> </td>
   <td><p>後処理に送信される XDP ドキュメントのパラメーター名</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>リダイレクト URL パラメーター名</p> </td>
   <td><p>後処理から送信されたリダイレクト URL のパラメーター名。この値は、任意の文字列変数名を指定できます。</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>PDF送信タイプ</p> </td>
   <td><p>PDF送信の種類 ( 通信を作成アプリケーションからの送信時に生成されるPDFの種類 )</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>インタラクティブ/非インタラクティブ</p> </td>
  </tr>
  <tr>
   <td><p>データ辞書インスタンスの最適化</p> </td>
   <td><p>サーバーとクライアントの間で最適化されたデータ辞書インスタンスの転送を有効にします</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>不整合の自動修正 </p> </td>
   <td><p>有効にすると、「レターの割り当て」で自動的に不整合を処理します</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>設定済みのデータ形式を使用</p> </td>
   <td><p>設定済みのデータ編集形式とデータ表示形式を使用するかどうかを制御します</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>データの表示形式</p> </td>
   <td><p>データのロケール固有の表示形式を指定します</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=truelocale=de_DE; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator= truelocale=ja_JP; dateFormat=dd-MM-yyyyyyy; numberDimalSeparator=; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>--</p> </td>
  </tr>
  <tr>
   <td><p>データ編集形式</p> </td>
   <td><p>データの形式を編集します。 これは、データを文字列として書き込む場合、または文字列からデータを解析する場合に使用されます</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>--<p> </p> </td>
  </tr>
  <tr>
   <td><p>発行時にレターインスタンスを管理</p> </td>
   <td><p>「レターを管理」機能を有効/無効にします（発行サーバーのみに適用）</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>監査の有効化</p> </td>
   <td><p>監査機能の有効化/無効化 false の場合、すべてのアクションの監査ログは無効になります</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>「監査の読み取り」の有効化</p> </td>
   <td><p>アセット読み取りの監査機能の有効化/無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>「監査の作成」を有効にする</p> </td>
   <td><p>アセット作成の監査機能の有効化/無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>「監査の更新」を有効にする</p> </td>
   <td><p>アセット更新の監査機能の有効化/無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>「監査を元に戻す」の有効化</p> </td>
   <td><p>アセット復帰の監査機能の有効化/無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>「監査を公開」の有効化</p> </td>
   <td><p>アセット公開の監査機能の有効化/無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>SaveAsDraft 監査の有効化</p> </td>
   <td><p>レタードラフト保存の監査機能の有効化/無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>「監査の送信」を有効にする</p> </td>
   <td><p>レター送信の監査機能の有効化/無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>メール監査の有効化</p> </td>
   <td><p>レターを電子メールで送信する監査機能の有効化/無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>「監査の印刷」の有効化</p> </td>
   <td><p>レター印刷の監査機能の有効化/無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>カスタム配信監査の有効化</p> </td>
   <td><p>レターのカスタム配信の監査機能の有効化/無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>添付ドキュメントのパラメーター名</p> </td>
   <td><p>後処理に送信された添付ドキュメントのパラメーター名</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>CM ユーザルート</p> </td>
   <td><p>すべての Correspondence Management ユーザーアセットを含むフォルダーの URL</p> </td>
   <td><p>--</p> </td>
   <td><p>有効なフォルダーの場所</p> </td>
  </tr>
  <tr>
   <td><p>レターキャッシュサイズ</p> </td>
   <td><p>キャッシュに保持するレターの最大数を指定します。</p> <p>この値を変更すると、 <code>in-memory</code> キャッシュ。</p> </td>
   <td><p>100</p> </td>
   <td><p>任意の数値</p> </td>
  </tr>
  <tr>
   <td><p>レターキャッシュを有効にする</p> </td>
   <td><p>レターキャッシュを有効または無効にします。</p> <p>この値を変更すると、 <code>in-memory </code> キャッシュ。</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>データ要素の順序</p> </td>
   <td><p>通信を作成インターフェイスで、レター内のデータ要素の順序を、順序に従って保持します</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>サポートの再読み込み</p> </td>
   <td><p>サーバー側でレンダリングされたレターのサポートの再読み込みを有効または無効にします。</p> <p>これを無効にすると、レターのレンダリングパフォーマンスが向上します。</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>一時フォルダー</td>
   <td>一時フォルダーの場所。</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>リモート保存</td>
   <td>レターインスタンスを指定した処理作成者に保存します。</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>互換性オプション</td>
   <td>configname:configvalue 形式の互換性オプションをコンマで区切って指定します。</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>Debug ディレクトリ </p> <p> </p> </td>
   <td>デバッグ用のファイルシステムフォルダの場所。 ディレクトリが <code>exists</code>の場合、デバッグダンプは生成されません。</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
