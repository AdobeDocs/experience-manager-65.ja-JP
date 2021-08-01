---
title: WS-securityヘッダーを使用して資格情報を渡す方法を教えてください。
description: WS-securityヘッダーを使用して資格情報を渡す方法を説明します
source-git-commit: 730ae7cd6cd04eb6377b37eafe29db597e93cce3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# JEE上のAEM Forms Custom DSCを使用したファイルの圧縮と解凍 {#compressing-decompressing-files}

## 必要な知識 {#prerequisites}

JEE上のAEM Forms Process Management、基本的なJavaプログラミング、およびカスタムコンポーネントの作成の経験。

**その他の必要な製品**

[Eclipse](https://www.eclipse.org/)や[Netbeans IDE](https://netbeans.apache.org/)などのJavaエディタ

## ユーザーレベル {#user-level}

中級者

JEE上のAEM Formsでは、カスタムDSC（ドキュメントサービスコンテナ）を作成して、追加設定なしで強化された機能を作成できます。 このようなコンポーネントの作成は、JEE上のAEM Formsランタイム環境にプラグ可能で、意図した目的を果たします。 この記事では、カスタムZIPサービスを作成する方法を説明します。このサービスを使用して、ファイルのリストを.zipファイルに圧縮し、.zipをドキュメントのリストに解凍します。

## カスタムDSCコンポーネントの作成 {#create-custom-dsc-component}

2つのサービス操作を持つカスタムDSCコンポーネントを作成し、ドキュメントのリストを圧縮および解凍します。 このコンポーネントは、圧縮と解凍にjava.util.zipパッケージを使用します。 次の手順に従って、カスタムコンポーネントを作成します。

1. adobe-livecycle-client.jarファイルをライブラリに追加します。
1. 必要なアイコンの追加
1. パブリッククラスの作成
1. UnzipDocumentおよびZipDocumentsという2つのパブリックメソッドを作成します。
1. 圧縮と解凍のロジックを記述します。

コードは次の場所にあります。

```java
/*
 * Custom DSC : ZIP Utility
 * Purpose: This is a LiveCycle ES2 custom component used to Compress & Decompress List of Documents
 * Author: Nithiyanandam Dharmadass
 * Organization: Ministry of Finance, Kingdom of Bahrain
 * Last modified Date: 18/Apr/2011
 */
package nith.lces2.dsc;

import java.util.zip.ZipEntry;
import java.util.zip.ZipInputStream;
import com.adobe.idp.Document;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.List;
import java.util.zip.ZipOutputStream;

public class ZIPService {

    static final int BUFFER = 2048; // 2MB buffer size

    public java.util.List UnzipDocument(com.adobe.idp.Document zipDocument) throws Exception {
        ZipInputStream zis = new ZipInputStream(zipDocument.getInputStream());

        ZipEntry zipFile;

        List resultList = new ArrayList();

        while ((zipFile = zis.getNextEntry()) != null) {

            ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();

            int count;  // an int variable to hold the number of bytes read from input stream
            byte data[] = new byte[BUFFER];
            while ((count = zis.read(data, 0, BUFFER)) != -1) {
                byteArrayOutStream.write(data, 0, count);   // write to byte array
            }

            com.adobe.idp.Document unzippedDoc = new Document(byteArrayOutStream.toByteArray());  // create an idp document
            unzippedDoc.setAttribute("file", zipFile.getName());
            unzippedDoc.setAttribute("wsfilename", zipFile.getName());  // update the wsfilename attribute
            resultList.add(unzippedDoc);
        }
        return resultList;  // List of uncompressed documents
    }

    public com.adobe.idp.Document ZipDocuments(java.util.List listOfDocuments,java.lang.String zipFileName) throws Exception {

        if (listOfDocuments == null || listOfDocuments.size() == 0) {
            return null;
        }

        ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();
        ZipOutputStream zos = new ZipOutputStream(byteArrayOutStream);  // ZIP Output Stream

        for (int i = 0; i < listOfDocuments.size(); i++) {
            Document doc = (Document) listOfDocuments.get(i);
            InputStream docInputStream = doc.getInputStream();
            ZipEntry zipEntry = new ZipEntry(doc.getAttribute("file").toString());
            zos.putNextEntry(zipEntry);
            int count;
            byte data[] = new byte[BUFFER];
            while ((count = docInputStream.read(data, 0, BUFFER)) != -1) {
                zos.write(data, 0, count);  // Read document content and add to zip entry
            }
            zos.closeEntry();
        }
        zos.flush();
        zos.close();

        Document zippedDoc = new Document(byteArrayOutStream.toByteArray());
        if(zipFileName==null || zipFileName.equals(""))
        {
            zipFileName = "CompressedList.zip";
        }
        zippedDoc.setAttribute("file", zipFileName);
        return zippedDoc;
    }
}
```

## Component.XMLファイルの作成 {#create-component-xml-file}

component.xmlファイルは、サービス操作とそのパラメーターを定義したパッケージのルートフォルダー内に作成する必要があります。

component.xmlファイルは次のように表示されます。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<component xmlns="http://adobe.com/idp/dsc/component/document">
<!-- Unique id identifying this component -->
   <component-id>ZipService</component-id>

<!-- Version -->
   <version>1.0</version>

<!-- Start of the Service definition -->
   <services>
<!-- Unique name for service descriptor.
           The value is used as the default name for
           deployed services -->
      <service name="ZipService">
<!-- service implementation class definition -->
        <implementation-class>nith.lces2.dsc.ZIPService</implementation-class>

<!-- description -->
        <description>Compress or Decompress list of documents</description>

<!--  You can provide your own icons for a distinct look   -->
          <small-icon>icons/Zip_icon16.png</small-icon>
          <large-icon>icons/Zip_icon32.png</large-icon>


<!-- automatically deploys the service and starts it after installation -->
         <auto-deploy service-id="ZipService" />

         <operations>
<!-- method name in the interface setSmtpHost-->
            <operation name="UnzipDocument">
<!-- input parameters to the "send" method -->
              <input-parameter name="zipDocument" title="Input ZIP Document" type="com.adobe.idp.Document">
                    <hint>A ZIP File to be decompressed</hint>
                </input-parameter>
                <output-parameter name="resultList" title="Decompressed list of documents" type="java.util.List">
                    <hint>Decompressed ZIP list</hint>
                </output-parameter>
            </operation>
            <operation name="ZipDocuments">
<!-- input parameters to the "send" method -->
              <input-parameter name="listOfDocuments" title="List of Documents" type="java.util.List">
                    <hint>A list of documents to be Compressed</hint>
                </input-parameter>
                <input-parameter name="zipFileName" title="Result File Name" type="java.lang.String">
                    <hint>The name of compressed file (optional)</hint>
                </input-parameter>

                <output-parameter name="zippedDoc" title="Compressed Zip file" type="com.adobe.idp.Document">
                    <hint>Compressed ZIP File</hint>
                </output-parameter>
            </operation>
             </operations>
      </service>
   </services>
</component>
```

## コンポーネントのパッケージ化とデプロイ {#packaging-deploying-component}

1. Javaプロジェクトをコンパイルし、.JARファイルを作成します。
1. Workbenchを使用して、JEE上のAEM Formsランタイムにコンポーネント（.JARファイル）をデプロイします。
1. Workbenchからサービスを開始します（下図を参照）。

![プロセスデザイン](assets/process-design.jpg)

## ワークフローでのZIPサービスの使用 {#using-zip-service-in-workflows}

カスタムサービスのUnzipDocument操作で、ドキュメント変数を入力として受け取り、ドキュメント変数のリストを出力として返すことができるようになりました。

![ドキュメントを解凍](assets/unzip-doc.jpg)

同様に、カスタムコンポーネントのZipDocuments操作では、ドキュメントのリストを入力として受け付け、それらをzipファイルとして圧縮して、圧縮ドキュメントを返すことができます。

![Zipドキュメント](assets/zip-doc.jpg)

次のワークフローオーケストレーションは、指定されたZIPファイルを解凍し、圧縮して別のZIPファイルに戻し、出力を返す方法を示します（下図を参照）。

![Zipを解凍ワークフロー](assets/unzip-zip-process.jpg)

## 一部のビジネスユースケース {#business-use-cases}

このZIPサービスは、次の使用例で使用できます。

* 指定したフォルダー内のすべてのファイルを検索し、圧縮ドキュメントとして返します。

* PDFドキュメントを解凍した後にReader用に拡張できるPDFドキュメントを多数含むZIPファイルを指定します。 これには、JEE上のAEM FormsReader拡張モジュールが必要です。

* Generate PDFサービスを使用して圧縮解除およびPDFドキュメントに変換できる、異種のドキュメントを含むZIPファイルを指定します。

* ポリシーでドキュメントのリストを保護し、ZIPファイルとして返します。

* ユーザーがプロセスインスタンスのすべての添付ファイルを1つのZIPファイルとしてダウンロードできるようにします。



