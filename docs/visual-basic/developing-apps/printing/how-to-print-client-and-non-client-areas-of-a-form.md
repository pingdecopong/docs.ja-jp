---
title: '方法: フォームのクライアント領域と非クライアント領域を印刷する (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- title bar [Visual Basic], printing
- printing
- borders [Visual Basic], printing
- entire form
- non-client area [Visual Basic], printing
ms.assetid: 856bb0e4-dbc3-47e2-81cd-4b376cf07757
ms.openlocfilehash: 566cf295462945a6bc90bc96f8907de34646bd00
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33584743"
---
# <a name="how-to-print-client-and-non-client-areas-of-a-form-visual-basic"></a>方法: フォームのクライアント領域と非クライアント領域を印刷する (Visual Basic)
<xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> コンポーネントを使用すると、 <xref:System.Drawing.Printing.PrintDocument> コンポーネントを使わなくても、画面に表示されているとおりにフォームのイメージをすぐに印刷することができます。 次の手順では、クライアント領域と非クライアント領域の両方を含むフォームを印刷する方法を示します。 非クライアント領域にはタイトル バー、境界、およびスクロール バーが含まれます。  
  
 PowerPack コントロールは、Visual Studio には含まれなくなりましたが、 [ダウンロード センター](http://www.microsoft.com/en-us/download/details.aspx?id=25169)からダウンロードできます。  
  
### <a name="to-print-both-the-client-and-the-non-client-areas-of-a-form"></a>フォームのクライアント領域と非クライアント領域の両方を印刷するには  
  
1.  **ツールボックス**で、 **[Visual Basic PowerPacks]** タブをクリックして、 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> コンポーネントをフォームにドラッグします。  
  
     <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> コンポーネントをコンポーネント トレイに追加します。  
  
2.  **[プロパティ]** ウィンドウで、 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A> プロパティを <xref:System.Drawing.Printing.PrintAction.PrintToPrinter>に設定します。  
  
3.  適切なイベント ハンドラー (たとえば [印刷] `Click` の `Button`イベント ハンドラー) に、次のコードを追加します。  
  
    ```  
    PrintForm1.Print(Me, PowerPacks.Printing.PrintForm.PrintOption.FullWindow)  
    ```  
  
    > [!NOTE]
    >  オペレーティング システムによっては、 <xref:System.Drawing.Graphics> メソッドによって描画されたテキストやグラフィックスが正しく印刷されないことがあります。 この場合は、互換性のある印刷メソッド `PrintForm1.Print(Me, PowerPacks.Printing.PrintForm.PrintOption.CompatibleModeFullWindow`を使用してください。  
  
## <a name="see-also"></a>関連項目  
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>  
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>  
 [PrintForm コンポーネント](../../../visual-basic/developing-apps/printing/printform-component.md)  
 [方法: スクロール可能フォームを印刷する](../../../visual-basic/developing-apps/printing/how-to-print-a-scrollable-form.md)
