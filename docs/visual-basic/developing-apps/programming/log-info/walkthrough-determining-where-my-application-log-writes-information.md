---
title: "チュートリアル: My.Application.Log による情報の書き込み先の確認 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Log オブジェクト, 出力場所"
  - "出力, アプリケーション ログ位置"
  - "My.Application.Log オブジェクト, 出力場所"
  - "イベント ログ, 出力場所の確認"
  - "アプリケーション イベント ログ, 出力場所"
  - "アプリケーション [Visual Basic], 出力場所"
ms.assetid: 5b70143a-7741-45f2-ae1d-03324a3a4189
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# チュートリアル: My.Application.Log による情報の書き込み先の確認 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

`My.Application.Log` オブジェクトは、複数のログ リスナーに情報を書き込むことができます。 ログ リスナーは、コンピューターの構成ファイルで設定し、アプリケーションの構成ファイルでオーバーライドできます。 このトピックでは、既定の設定について、およびアプリケーションの設定を確認する方法について説明します。  
  
 既定の出力場所の詳細については、「[アプリケーション ログの使用](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)」を参照してください。  
  
### My.Application.Log のリスナーを確認するには  
  
1.  アセンブリの構成ファイルを見つけます。 アセンブリを開発中の段階では、**ソリューション エクスプローラー**から [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs-md.md)] の app.config にアクセスできます。 開発が終了すると、構成ファイルはアセンブリの名前に ".config" を付け加えたファイル名で、アセンブリと同じディレクトリに配置されています。  
  
    > [!NOTE]
    >  アセンブリによっては、構成ファイルがない場合もあります。  
  
     構成ファイルは XML ファイルです。  
  
2.  `<sources>` セクション内にある、`name` 属性が "DefaultSource" の `<source>` セクションで、`<listeners>` セクションを見つけます。`<sources>` セクションは、最上位の `<configuration>` セクション内の `<system.diagnostics>` セクションにあります。  
  
     これらのセクションがない場合には、`My.Application.Log` のログ リスナーは、コンピューターの構成ファイルで設定されている可能性があります。 以下の手順は、コンピューターの構成ファイルの定義を確認する方法の説明です。  
  
    1.  コンピューターの machine.config ファイルを見つけます。 通常は、*SystemRoot\\Microsoft.NET\\Framework\\frameworkVersion\\CONFIG* ディレクトリにあります。`SystemRoot` はオペレーティング システム ディレクトリ、`frameworkVersion` は [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] のバージョンです。  
  
         machine.config の設定は、アプリケーションの構成ファイルでオーバーライドできます。  
  
         以下に示すオプションの要素が存在しない場合には、自分で作成できます。  
  
    2.  最上位の `<configuration>` セクション内にある `<system.diagnostics>` セクション内の `<sources>` セクションで、`name` 属性が "DefaultSource" の `<source>` セクション内の `<listeners>` セクションを見つけます。  
  
         これらのセクションがない場合、`My.Application.Log` にあるのは既定のログ リスナーのみです。  
  
3.  \<`listeners>` セクションで \<`add>` 要素を見つけます。  
  
     これらの要素は、名前付きのログ リスナーを `My.Application.Log` のソースに追加します。  
  
4.  最上位の `<configuration>` セクション内にある `<system.diagnostics>` セクション内の `<sharedListeners>` セクションで、ログ リスナーの名前の `<add>` 要素を見つけます。  
  
5.  多くの型の共有リスナーでは、リスナーがデータを書き込む先は、リスナーの初期化データで指定されています。  
  
    -   <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener?displayProperty=fullName> リスナーは、導入部で説明したように、ファイル ログに書き込みます。  
  
    -   <xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName> リスナーは、`initializeData` パラメーターで指定された、コンピューターのイベント ログに情報を書き込みます。 イベント ログを参照するには、**サーバー エクスプローラー**または **Windows イベント ビューアー**を使用できます。 詳細については、「[.NET Framework の ETW イベント](../Topic/ETW%20Events%20in%20the%20.NET%20Framework.md)」を参照してください。  
  
    -   <xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=fullName> リスナーおよび <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=fullName> リスナーは、`initializeData` パラメーターで指定されたファイルに書き込みます。  
  
    -   <xref:System.Diagnostics.ConsoleTraceListener?displayProperty=fullName> リスナーは、コマンド ライン コンソールに書き込みます。  
  
    -   他の型のログ リスナーが情報を書き込む先については、その型のドキュメントを参照してください。  
  
## 参照  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 <xref:System.Diagnostics.DefaultTraceListener>   
 <xref:System.Diagnostics.EventLogTraceListener>   
 <xref:System.Diagnostics.DelimitedListTraceListener>   
 <xref:System.Diagnostics.XmlWriterTraceListener>   
 <xref:System.Diagnostics.ConsoleTraceListener>   
 <xref:System.Diagnostics>   
 [アプリケーション ログの使用](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [How to: Log Exceptions](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)   
 [方法: ログ メッセージを書き込む](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)   
 [チュートリアル : My.Application.Log による情報の書き込み先の変更](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)   
 [.NET Framework の ETW イベント](../Topic/ETW%20Events%20in%20the%20.NET%20Framework.md)   
 [Troubleshooting: Log Listeners](../../../../visual-basic/developing-apps/programming/log-info/troubleshooting-log-listeners.md)