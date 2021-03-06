---
title: NoPersistScope アクティビティ
ms.date: 03/30/2017
ms.assetid: 9a0baeb7-a05c-4fac-b905-252758cb71bb
ms.openlocfilehash: e4779bf28fc2fc1341cce5134a872b108278611c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33516440"
---
# <a name="nopersistscope-activity"></a>NoPersistScope アクティビティ
このサンプルでは、ワークフローでシリアル化不可能で破棄可能な状態を処理する方法を示します。 ワークフローでシリアル化不可能な状態を永続化しないようにし、破棄可能なオブジェクトをワークフローで使用した後にクリーンアップすることが重要です。  
  
## <a name="demonstrates"></a>使用例  
 `NoPersistScope` カスタム アクティビティおよびデザイナー。  
  
## <a name="using-the-nopersistzone-activity"></a>NoPersistZone アクティビティの使用  
 サンプル ワークフローの実行時に、`CreateTextWriter` というカスタム アクティビティによって、<xref:System.IO.TextWriter> 型のオブジェクトが作成されてワークフロー変数に保存されます。 <xref:System.IO.TextWriter> は <xref:System.IDisposable> オブジェクトです。 この <xref:System.IO.TextWriter> は、サンプルが実行されるディレクトリにある out.txt という名前のファイルに書き込むように構成されており、コンソールで入力するテキストをエコーするときに <xref:System.Activities.Statements.WriteLine> アクティビティによって使用されます。  
  
 エコー ロジックは、ワークフローが永続化されないようにする `NoPersistScope` アクティビティ (このサンプルの一部でもあるコード) 内で実行されます。 入力した場合`unload`コンソールで、ホストはワークフロー インスタンスを永続化を試みますが、ワークフロー内に留まるので、この操作がタイムアウト、`NoPersistScope`です。 また、ワークフローは `Dispose` というカスタム アクティビティを使用して、<xref:System.IO.TextWriter> オブジェクトを使い終わったら破棄します。 `Dispose` アクティビティは、Try ブロックの実行中に例外が発生した場合でも実行されるように、<xref:System.Activities.Statements.TryCatch.Finally%2A> 変数が宣言される <xref:System.Activities.Statements.TryCatch> アクティビティの <xref:System.IO.TextWriter> ブロック内に配置されます。  
  
 入力できます`exit`をワークフロー インスタンスを完了し、プログラムを終了します。  
  
#### <a name="to-run-the-sample"></a>サンプルを実行するには  
  
1.  [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] で NoPersistZone.sln ソリューションを開きます。  
  
2.  ソリューションをビルドするには、ctrl キーと shift キーを押しながら B キーを押してまたは選択**ソリューションのビルド**から、**ビルド**メニュー。  
  
3.  F5 キーを押してビルドが成功した後、または選択**デバッグの開始**から、**デバッグ**メニューまたは、ctrl キーを押しながら f5 キーを押してまたは選択**デバッグなしで開始**から、**デバッグ** メニューの デバッグなしで実行します。  
  
#### <a name="to-cleanup-optional"></a>クリーンアップするには (省略可能)  
  
1.  SQL インスタンス ストアを削除するには、Cleanup.cmd を実行します。  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合に、 [Windows Communication Foundation (WCF) および .NET Framework 4 向けの Windows Workflow Foundation (WF) サンプル](http://go.microsoft.com/fwlink/?LinkId=150780)すべて Windows Communication Foundation (WCF) をダウンロードして[!INCLUDE[wf1](../../../../includes/wf1-md.md)]サンプルです。 このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\NoPersistScope`