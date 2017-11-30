---
title: "ISymUnmanagedSymbolSearchInfo::GetSearchPathLength メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ISymUnmanagedSymbolSearchInfo.GetSearchPathLength
api_location: diasymreader.dll
api_type: COM
f1_keywords: ISymUnmanagedSymbolSearchInfo::GetSearchPathLength
helpviewer_keywords:
- GetSearchPathLength method [.NET Framework debugging]
- ISymUnmanagedSymbolSearchInfo::GetSearchPathLength method [.NET Framework debugging]
ms.assetid: 274e73cf-8333-47ba-ac12-70214e2b0112
topic_type: apiref
caps.latest.revision: "7"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 58a788d8ef96a52c0b1bc361a97013f27c2809da
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="isymunmanagedsymbolsearchinfogetsearchpathlength-method"></a><span data-ttu-id="78beb-102">ISymUnmanagedSymbolSearchInfo::GetSearchPathLength メソッド</span><span class="sxs-lookup"><span data-stu-id="78beb-102">ISymUnmanagedSymbolSearchInfo::GetSearchPathLength Method</span></span>
<span data-ttu-id="78beb-103">検索パスの長さを取得します。</span><span class="sxs-lookup"><span data-stu-id="78beb-103">Gets the search path length.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="78beb-104">構文</span><span class="sxs-lookup"><span data-stu-id="78beb-104">Syntax</span></span>  
  
```  
HRESULT GetSearchPathLength(  
    [out] ULONG32 *pcchPath);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="78beb-105">パラメーター</span><span class="sxs-lookup"><span data-stu-id="78beb-105">Parameters</span></span>  
 `pcchPath`  
 <span data-ttu-id="78beb-106">[out]ポインター、`ULONG32`検索パスの長さを格納するために必要なバッファーの文字のサイズを受け取る。</span><span class="sxs-lookup"><span data-stu-id="78beb-106">[out] A pointer to a `ULONG32` that receives the size, in characters, of the buffer required to contain the search path length.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="78beb-107">戻り値</span><span class="sxs-lookup"><span data-stu-id="78beb-107">Return Value</span></span>  
 <span data-ttu-id="78beb-108">メソッドが成功した場合は S_OK、それ以外の場合、E_FAIL またはその他のエラー コード。</span><span class="sxs-lookup"><span data-stu-id="78beb-108">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="78beb-109">要件</span><span class="sxs-lookup"><span data-stu-id="78beb-109">Requirements</span></span>  
 <span data-ttu-id="78beb-110">**ヘッダー:** CorSym.idl、CorSym.h</span><span class="sxs-lookup"><span data-stu-id="78beb-110">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="78beb-111">関連項目</span><span class="sxs-lookup"><span data-stu-id="78beb-111">See Also</span></span>  
 [<span data-ttu-id="78beb-112">ISymUnmanagedSymbolSearchInfo インターフェイス</span><span class="sxs-lookup"><span data-stu-id="78beb-112">ISymUnmanagedSymbolSearchInfo Interface</span></span>](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedsymbolsearchinfo-interface.md)