---
title: '方法: オブジェクトの遅延初期化を実行する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- lazy initialization in .NET, how to perform
ms.assetid: 8cd68620-dcc3-4f20-8835-c728a6820e71
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9d33dcb2b060d1d453ae17a48d2765d489de0038
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33394476"
---
# <a name="how-to-perform-lazy-initialization-of-objects"></a>方法: オブジェクトの遅延初期化を実行する
<xref:System.Lazy%601?displayProperty=nameWithType> クラスは、オブジェクトの遅延初期化とインスタンス化を実行する操作を簡略化します。 オブジェクトを限定的に初期化すれば、不要なオブジェクトを作成する必要がなくなります。また、オブジェクトに初めてアクセスするときまで、そのオブジェクトの初期化を延期できます。 詳細については、「[限定的な初期化](../../../docs/framework/performance/lazy-initialization.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Lazy%601> で値を初期化する方法を示します。 `someCondition` 変数を true または false に設定する他の一部のコードでは、遅延変数は必要ないものとします。  
  
```vb  
Dim someCondition As Boolean = False  
  
Sub Main()  
    'Initializing a value with a big computation, computed in parallel  
    Dim _data As Lazy(Of Integer) = New Lazy(Of Integer)(Function()  
                                                             Dim result =  
                                                                 ParallelEnumerable.Range(0, 1000).  
                                                                 Aggregate(Function(x, y)  
                                                                               Return x + y  
                                                                           End Function)  
                                                             Return result  
                                                         End Function)  
  
    '  do work that may or may not set someCondition to True  
    ' ...  
    '  Initialize the data only if needed  
    If someCondition = True Then  
  
        If (_data.Value > 100) Then  
  
            Console.WriteLine("Good data")  
        End If  
    End If  
End Sub  
```  
  
```csharp  
  static bool someCondition = false;    
  //Initializing a value with a big computation, computed in parallel  
  Lazy<int> _data = new Lazy<int>(delegate  
  {  
      return ParallelEnumerable.Range(0, 1000).  
          Select(i => Compute(i)).Aggregate((x,y) => x + y);  
  }, LazyExecutionMode.EnsureSingleThreadSafeExecution);  
  
  // Do some work that may or may not set someCondition to true.  
  //  ...  
  // Initialize the data only if necessary  
  if (someCondition)  
{  
    if (_data.Value > 100)  
      {  
          Console.WriteLine("Good data");  
      }  
}  
```  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Threading.ThreadLocal%601?displayProperty=nameWithType> クラスを使用して、現在のスレッド上の現在のオブジェクト インスタンスでのみ表示される型を初期化する方法を示します。  
  
 [!code-csharp[CDS#13](../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/cds2.cs#13)]
 [!code-vb[CDS#13](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/lazyhowto.vb#13)]  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Threading.LazyInitializer?displayProperty=nameWithType>  
 [遅延初期化](../../../docs/framework/performance/lazy-initialization.md)
