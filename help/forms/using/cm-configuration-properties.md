---
title: Correspondence Management設定プロパティ
seo-title: Correspondence Management設定プロパティ
description: このトピックでは、ソリューションごとの設定でAsset Composerを変更する方法について説明します。このトピックでは、編集可能なプロパティの説明、デフォルト値および指定できる値などの詳細について説明します。
seo-description: このトピックでは、ソリューションごとの設定でAsset Composerを変更する方法について説明します。このトピックでは、編集可能なプロパティの説明、デフォルト値および指定できる値などの詳細について説明します。
uuid: 6b401d51-9332-459b-b751-42a9b5a1462d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: f2955419-c680-44a7-9913-c594b4577551
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 96%

---


# Correspondence Management設定プロパティ {#correspondence-management-configuration-properties}

これらのプロパティを設定するには、ブラウザーで次のURLを開きます。`https://<server>:<port>/<contextPath>/system/console/configMgr`を選択し、**Correspondence Management設定**&#x200B;を選択します。

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
   <td><p>12.7 mm</p> </td>
   <td><p>任意の数値</p> </td>
  </tr>
  <tr>
   <td>最小幅の数字</td>
   <td>ローマ数字以外の番号付きリストに適用する、箇条書き／番号フィールドの最小幅</td>
   <td>8.0 mm</td>
   <td>任意の数値</td>
  </tr>
  <tr>
   <td><p>最小幅のローマ数字</p> </td>
   <td><p>ローマ数字以外の番号付きリストに適用する、箇条書き／番号フィールドの最小幅</p> </td>
   <td><p>12.7 mm</p> </td>
   <td><p>任意の数値</p> </td>
  </tr>
  <tr>
   <td>レンディションタイプ</td>
   <td>通信を作成アプリケーションがレターのプレビューをレンダリングするレンディションタイプです。 </td>
   <td>HTML レンダリング</td>
   <td>HTML レンダリング／PDF レンダリング</td>
  </tr>
  <tr>
   <td><p>CCR PDF ハイライトを有効化</p> </td>
   <td><p>通信の作成アプリケーションにおいてPDF上のハイライト表示を有効にします。</p> </td>
   <td><p>true</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>対象のハイライトの種類</p> </td>
   <td><p>通信を作成アプリケーションでの対象のハイライトの種類</p> </td>
   <td><p>border</p> </td>
   <td><p>境界線／塗りつぶし／なし</p> </td>
  </tr>
  <tr>
   <td><p>対象のハイライトの色</p> </td>
   <td><p>通信を作成アプリケーションでの対象のハイライトの色</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>任意の RGB カラー（R、G、B の形式）</p> </td>
  </tr>
  <tr>
   <td><p>コンテンツのハイライトの種類</p> </td>
   <td><p>通信を作成アプリケーションでのコンテンツのハイライトの種類</p> </td>
   <td><p>塗りつぶし</p> </td>
   <td><p>境界線／塗りつぶし／なし</p> </td>
  </tr>
  <tr>
   <td><p>対象のハイライトの色</p> </td>
   <td><p>通信を作成アプリケーションでのコンテンツのハイライトの色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>任意の RGB カラー（R、G、B の形式）</p> </td>
  </tr>
  <tr>
   <td><p>フィールドのハイライトの種類</p> </td>
   <td><p>通信を作成アプリケーションでのフィールドのハイライトの種類</p> </td>
   <td><p>塗りつぶし</p> </td>
   <td><p>境界線／塗りつぶし／なし</p> </td>
  </tr>
  <tr>
   <td><p>フィールドのハイライトの色</p> </td>
   <td><p>通信を作成アプリケーションでのフィールドのハイライトの色</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>任意の RGB カラー（R、G、B の形式）</p> </td>
  </tr>
  <tr>
   <td><p>アプリケーションのタイムアウト</p> </td>
   <td><p>アプリケーションのタイムアウト（秒数）</p> </td>
   <td><p>1200</p> </td>
   <td><p>任意の数値</p> </td>
  </tr>
  <tr>
   <td><p>PDF ドキュメントのパラメーター名</p> </td>
   <td><p>後処理での PDF ドキュメントのパラメーター名</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>XML ドキュメントのパラメーター名</p> </td>
   <td><p>後処理での XML ドキュメント（データ）のパラメーター名</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>XDP ドキュメントのパラメーター名</p> </td>
   <td><p>後処理に送信された XDP ドキュメントのパラメーター名</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>リダイレクト URL パラメーター名</p> </td>
   <td><p>後処理から送信されたリダイレクト URL パラメーター名。この値は任意の文字列変数名を設定できます</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>PDF 送信の種類</p> </td>
   <td><p>PDF 送信の種類（通信を作成アプリケーションからの送信時に生成される PDF の種類）</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>インタラクティブ／非インタラクティブ</p> </td>
  </tr>
  <tr>
   <td><p>データディクショナリインスタンスの最適化</p> </td>
   <td><p>サーバーとクライアントの間で最適化されたデータディクショナリインスタンスを有効化します</p> </td>
   <td><p>true</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>不整合の自動修正 </p> </td>
   <td><p>有効化すると、「レターの割り当て」で自動的に不整合を処理します</p> </td>
   <td><p>true</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>設定済みのデータ形式を使用</p> </td>
   <td><p>「設定済みデータ編集形式とデータ表示形式」を使用するか制御します</p> </td>
   <td><p>true</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>日付の表示形式</p> </td>
   <td><p>データのロケール固有表示を指定します</p> </td>
   <td><p>locale=ja_JP; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=truelocale=de_DE; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=ja_JP; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>日付の編集形式</p> </td>
   <td><p>データの編集形式これは、データを文字列として書き込む、または文字列から解析する場合に使用されます</p> </td>
   <td><p>locale=ja_JP; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.;numberGroupSeparator=,;numberUseGroupSeparator=true</p> </td>
   <td>—<p> </p> </td>
  </tr>
  <tr>
   <td><p>「発行」でレターインスタンスを管理</p> </td>
   <td><p>レターの管理機能の有効化／無効化（パブリッシュサーバーのみに適用）</p> </td>
   <td><p>false</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>「監査」の有効化</p> </td>
   <td><p>監査機能の有効化／無効化false の場合、すべての操作の監査ログは無効化されます</p> </td>
   <td><p>false</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>「監査の読み取り」の有効化</p> </td>
   <td><p>アセット読み取りの監査機能の有効化／無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>「監査の作成」を有効化</p> </td>
   <td><p>アセット作成の監査機能の有効化／無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>「監査の更新」の有効化</p> </td>
   <td><p>アセット更新の監査機能の有効化／無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>「監査の復帰」の有効化</p> </td>
   <td><p>アセット復帰の監査機能の有効化／無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>「監査の発行」の有効化</p> </td>
   <td><p>アセット発行の監査機能の有効化／無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>「SaveAsDraft 監査」の有効化</p> </td>
   <td><p>レタードラフト保存の監査機能の有効化／無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>「監査の送信」の有効化</p> </td>
   <td><p>レター送信の監査機能の有効化／無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>「監査を電子メール送信」の有効化</p> </td>
   <td><p>レターを電子メール送信の監査機能の有効化／無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>「監査の印刷」の有効化</p> </td>
   <td><p>レター印刷の監査機能の有効化／無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>「監査のカスタム配信」の有効化</p> </td>
   <td><p>レターのカスタム配信の監査機能の有効化／無効化</p> </td>
   <td><p>false</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>添付ドキュメントパラメーター名</p> </td>
   <td><p>後処理に送信された添付ドキュメントのパラメーター名</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>CM ユーザールート</p> </td>
   <td><p>すべてのCorrespondence Managementユーザーアセットを含むフォルダーのURL</p> </td>
   <td><p>—</p> </td>
   <td><p>有効なフォルダーの位置</p> </td>
  </tr>
  <tr>
   <td><p>レターのキャッシュサイズ</p> </td>
   <td><p>キャッシュに保存するレターの最大数を保存します。</p> <p>この値を変更すると、 <code>in-memory</code> cache.</p> </td>
   <td><p>100</p> </td>
   <td><p>数値</p> </td>
  </tr>
  <tr>
   <td><p>レターキャッシュの有効化</p> </td>
   <td><p>レターキャッシュを有効化または無効化します。</p> <p>この値を変更すると、  <code>in-memory </code> キャッシュ。</p> </td>
   <td><p>true</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>データ要素の順序</p> </td>
   <td><p>通信を作成インターフェイスでデータ要素の順序を、レターでの順序に従って保持します。</p> </td>
   <td><p>true</p> </td>
   <td><p>true ／ false</p> </td>
  </tr>
  <tr>
   <td><p>サポートを再読み込み</p> </td>
   <td><p>サーバー側でレンダリングされたサポートを有効化または無効化します。</p> <p>これを無効化するとレターのレンダリングパフォーマンスが向上します。</p> </td>
   <td><p>false</p> </td>
   <td><p>true ／ false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>一時フォルダー</td>
   <td>一時フォルダーの場所</td>
   <td>acm.tpmフォルダー</td>
   <td> </td>
  </tr>
  <tr>
   <td>リモート保存</td>
   <td>レターインスタンスを指定された処理中の作成者で保存します。</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>互換性オプション</td>
   <td>フォーマットの互換性オプション、configname:configvalueは、コンマで区切られています。</td>
   <td>acm.compatibilityオプション</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>Debugディレクトリ </p> <p> </p> </td>
   <td>デバッグのファイルシステムフォルダーの場所。ディレクトリが  <code>exists</code>に設定されていない場合、デバッグダンプは生成されません。</td>
   <td>acm.debugディレクトリ</td>
   <td> </td>
  </tr>
 </tbody>
</table>
